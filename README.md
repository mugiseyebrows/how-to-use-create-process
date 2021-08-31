# How to use CreateProcess WINAPI

Documentation for `CreateProcess` on [docs.microsoft.com](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-createprocessa) regarding `lpApplicationName` and `lpCommandLine` is very confusing, and fails to say the following:

There's two ways you can start process with `CreateProcess`: 
1) Using executable's full path.
2) Using executable's name.

For example you want to open `D:\dev` in `explorer`, 
you can either call 
1) `CreateProcess(NULL, "explorer D:\\dev", ...);`    
or 
2) `CreateProcess("C:\\Windows\\explorer.exe", "explorer D:\\dev", ...);`.

Notice that either way you need to specify app name as first argument in `lpCommandLine` so it can handle args correctly. If you dont - it's likely that app will lose first argument.

If you dont specify `lpApplicationName` (set it `NULL`), system tries to find app in executable directory, then in `PATH` environment variable, otherwise it just runs that specific file.

Use first form if you're not sure (or dont care) about `PATH` contents but sure about executable's path, use second form if you rely on user to setup correct environment or your executable is located in same directory.

See [test1.log](https://github.com/mugiseyebrows/test-create-process/blob/main/test1.log)
[test2.log](https://github.com/mugiseyebrows/test-create-process/blob/main/test2.log)
at [https://github.com/mugiseyebrows/test-create-process](https://github.com/mugiseyebrows/test-create-process) for details.

Note: buffer `lpCommandLine` should also be writable (not `const char*`) - not like in examples above (simplified for demonstration purposes - dont do that).