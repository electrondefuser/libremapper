## Library Remapper (libremapper) 
libremapper (a.k.a Library Remapper) is a library remapping system that prevents the scanning of suspicious libraries in the memory maps file. This can be used to enhance the security of applications by obscuring the memory layout and reducing the attack surface for malicious scanning tools. This is also helpful to hide instrumentation tool's injected libraries like Frida/DynamoRIO etc.
 
 ## Introduction 
 The memory maps file (`/proc/[pid]/maps`) provides information about the memory regions of a running process, including shared libraries and other dynamically allocated segments. Malicious actors may exploit this information to scan for and target specific libraries or memory regions in an application. **libremapper** seeks to mitigate such risks by remapping these suspicious libraries, making it harder for attackers to locate and identify them. It achieves this by performing manual remapping of libraries during runtime, effectively hiding them from common memory scanning techniques. 
 
 ## Features 
**Library Remapping**: Safeguards suspicious libraries by remapping them to different addresses. 
**Obfuscation**: Hides libraries and memory segments from basic scanning attempts.
**Customizable**: Configurable remapping patterns based on user-defined rules.
**Lightweight**: Efficient and minimal overhead, suitable for performance-sensitive applications. 

## Installation
To use **libremapper**, you can clone this repository and copy the two header files which are `remapper.h` and `log.h` in the you desired project directory and including them in the target project. Use the function `remap_lib` or `remap_all` to remap the target library.

## Usage
The remapper can me used very easily just by include the required header `remapper.h` in the needed C/C++ project and just calling the function `remap_lib` or `remap_all`.

## Example
**Single library remapping**
```cpp
#include "libremapper.h" 

int main(int argc, char** argv) { 
	const char* library_path = "/path/to/library.so"; 
	int result = remap_lib(library_path); 
	
	if (result == 0)
		printf("Library successfully remapped.\n"); 

	return 0; 
}
```

**Remapping multiple libraries**
```cpp
#include "libremapper.h" 
#include "vector"
#include "string"

int main(int argc, char** argv) { 
	std::vector<std::string> libraries;
	libraries.push_back("lib_01.so");
	libraries.push_back("lib_02.so");
	libraries.push_back("lib_03.so");
	
	int result = remap_all(libraries); 

	if (result == 0)
		printf("Libraries successfully remapped.\n"); 

	return 0; 
}
```

## Contributions
We welcome contributions from the community! If you’d like to contribute, please follow these steps:
1.  Fork the repository.
2.  Create a feature branch: `git checkout -b feature/my-feature`
3.  Commit your changes: `git commit -m 'Add some feature'`
4.  Push to the branch: `git push origin feature/my-feature`
5.  Open a pull request.
