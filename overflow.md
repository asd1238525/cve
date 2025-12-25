# Bus Ticketing System has buffer overflow in Bus Ticketing System.cpp

## supplier 
https://code-projects.org/stationary-shop-management-system-in-c-programming-with-source-code/

## Vulnerability file
Bus Ticketing System.cpp

## Description

**Code Analysis**

-Unbounded input into fixed-size character arrays causes buffer overflow (global buffer overflow):
```cpp
	class bus {
			char arriva[9], deprt[9], from[9], to[9], pname[99];
			int busn, dtym, tseat, fair, s;
			// ...
	} b[8];

	void bus::install() {
			// ...
			cin >> from; // no length limit; from[9] => max 8 chars + '\\0'
			cin >> to;   // no length limit; to[9]   => max 8 chars + '\\0'
			// ...
	}

	void bus::book() {
			// ...
			cin >> pname; // no length limit; pname[99]
			// ...
	}
```
Any input longer than the buffers (e.g., `from`/`to` > 8 characters or `pname` > 99 characters) overflows into adjacent members (`tseat`, `dtym`, `busn`, etc.) or even the next object in the global array.
Out-of-bounds write on the global array `b[8]`:
```cpp
	int p = 0;
	// ...
	b[p].install(); // no check for p < 8
	b[p].book();    // no check for p < 8
	// p++ in install(); the 9th install writes past b[7]
```
The 9th installation (when `p == 8`) writes beyond the array, corrupting memory.

- Risk-amplifying logic:
```cpp
	while ((b[n].tseat = b[n].tseat - s) < 0) {
			// state mutation inside condition; interacts badly with corrupted values
			b[n].tseat = b[n].tseat + s;
			// ...
	}
```

**Impact**
- Memory corruption leading to persistent data tampering (seat counts, departure time, bus number) and denial of service (crash).
- Potential information disclosure (unterminated C-strings may print past bounds).


## POC

Run the program → select "1 => Install".  
In the "From:" field, enter an extra-long word, for example 20 characters: AAAAAAAAAAAAAAAAAAAA (exceeding the 8-byte limit).
![image-2025](https://github.com/asd1238525/cve/blob/main/3153c8e4243e7dd5a3a89dae7ac59679.png)

**Result**
Program crash or abnormal behavior (depending on compiler / stack layout).
![image-2025](https://github.com/asd1238525/cve/blob/main/143fce4823f4debfb9299dea4cc8bbcf.png)