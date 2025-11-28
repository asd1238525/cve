# rental-management-system has CRLF Injection in Transacation.java

## supplier 
https://code-projects.org/rental-management-system-in-java-with-source-code/
## Vulnerability file
Transaction.java

## describe  

In Transaction.java, user-controlled input (for example: customer name, location or contact) is written directly into the transaction log file without any sanitization. If the input contains CR (\r) or LF (\n) characters, an attacker can inject additional lines into the log (a CRLF injection). This allows an attacker to tamper with audit records, insert forged entries, confuse parsers that consume the log, or—when exported to CSV/Excel—perform formula injection that may lead to client-side risks.

Root cause: the code concatenates and prints raw user strings (e.g. `outFile.println("Full Name: " + aCustomer.getFullName());`) without removing or escaping control characters.

Impact: injected newlines can split or fake log records (breaking integrity and trust of audit data), can break automated parsing or reporting pipelines, and can be weaponized when data is exported (CSV/Excel) to trigger formula execution on the client side. The correct mitigation is to sanitize or escape input before writing, prefer structured logging (JSON) or a database for records, and apply CSV/Excel-specific escaping for exports.

**Code analysis** 

Line 418-432 in Transaction.java

```java
	PrintWriter outFile = new PrintWriter(new FileOutputStream(new File("Transactions_Inventory.txt"), true));
        outFile.println("Current Date: " + getCurrentMonth() + " " + getCurrentDate() + ", " + getCurrentYear());
		outFile.println(" ");
		outFile.println("Pick up Date: " + getPickMonth() + " " + getPickDate() + ", " + getPickYear());
		outFile.println("Return Date: " + getReturnMonth() + " " + getReturnDate() + ", " + getReturnYear()  + " = Days: " + getDays());
		outFile.println("Full Name: " + aCustomer.getFullName());
		outFile.println("Age: " + getAge());
		outFile.println("Location: " + aCustomer.getLocation());
		outFile.println("Contact: " + aCustomer.getContact());
		outFile.println("Car: " + aCar.getCar());
		outFile.printf("Total Rent Price: %.2f", + getRentalPrice());
		outFile.println(" ");
		outFile.println("--------------------------------------------------");
        outFile.close();
     }
```


## POC

![image-2025](https://github.com/asd1238525/cve/blob/main/03e3af42-803c-4220-9966-74c5419ad934.png)

```text
Input (Full Name) submitted (literal with escaped newline):
Alice\nFAKE_LINE: injected

The program writes to `Transactions_Inventory.txt`. The tail of the file will contain the injected lines, for example:

Full Name: Alice
FAKE_LINE: injected Smith
```Injection

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/724235da-b410-44bf-b9dc-f44c7a4ee152.png)
Successfully CRLF Injection