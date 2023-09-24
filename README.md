# Windows-API-for-Red-Team

This repository is a compilation of the main Windows APIs for use in PenTest, Red Team operations and Malware Analysis

## CreateToolhelp32Snapshot 

The CreateToolhelp32Snapshot API is commonly used in C++ programming to enumerate processes and modules on Windows systems. Although it is not an API directly related to cybersecurity or pen testing, it can be used to obtain information about running processes, which can be useful in security contexts.

### Example Code

C++ 
```
#include <windows.h>
#include <tlhelp32.h>
#include <iostream>

int main() {
    //Create a snapshot of running processes
    HANDLE hSnapshot = CreateToolhelp32Snapshot(TH32CS_SNAPPROCESS, 0);
    if (hSnapshot == INVALID_HANDLE_VALUE) {
        std::cerr << "Erro ao criar o snapshot: " << GetLastError() << std::endl;
        return 1;
    }

    // Structure for storing information about a process
    PROCESSENTRY32 pe32;
    pe32.dwSize = sizeof(PROCESSENTRY32);

    // Initialize the loop to enumerate the processes
    if (Process32First(hSnapshot, &pe32)) {
        do {
            std::cout << "Processo ID: " << pe32.th32ProcessID << std::endl;
            std::cout << "Nome do processo: " << pe32.szExeFile << std::endl;
        } while (Process32Next(hSnapshot, &pe32));
    } else {
        std::cerr << "Erro ao enumerar processos: " << GetLastError() << std::endl;
    }

    // Close the snapshot
    CloseHandle(hSnapshot);

    return 0;
}
```
