# Section 10: Security & Permissions

## Script Injection
```
A value, set outside a Workflow, is used in a Workflow
Example(s):
    - Issue title used in a Workflow shell command
        -- Workflow / command behavior could be changed
```

## Malicious Third-Party Actions
```
Actions can perform any logic, including potentially malicious logic
Example(s):
    - A third-party Action that reads and exports your secrets
Solution(s):
    - Only use trusted Actions and inspect code of unknown / untrusted authors
```

## Permission Issues
```
Avoid overly permissive permissions (Least Privilege Principle)
Example(s):
    - Only allow checking out code ("read-only")
Solution(s):
    - GitHub Actions supports fine-grained permissions control
```