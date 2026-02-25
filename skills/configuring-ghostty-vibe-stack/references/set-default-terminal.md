# Set Ghostty as Default Terminal

Compile and run this Swift helper to make Ghostty the default terminal for "Open in Terminal" in Finder:

```bash
cat << 'SWIFT' > /tmp/set_default_terminal.swift
import CoreServices
let result = LSSetDefaultRoleHandlerForContentType(
    "public.unix-executable" as CFString, .shell,
    "com.mitchellh.ghostty" as CFString)
print(result == 0 ? "Success: Ghostty set as default terminal" : "Failed: \(result)")
SWIFT
swiftc /tmp/set_default_terminal.swift -o /tmp/set_default_terminal && /tmp/set_default_terminal
rm -f /tmp/set_default_terminal.swift /tmp/set_default_terminal
```
