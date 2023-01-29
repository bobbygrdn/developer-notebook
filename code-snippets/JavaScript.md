# Code Snippets

### Generate Password Function

```javascript
const generatePassword = () => {
    let password = "";
    let length = 16;

    const chars = `0123456789abcdefghijklmnopqrstuvwxyz!@#$%^&*()ABCDEFGHIJKLMNOPQRSTUVWXYZ`

    const arr = new Uint32Array(length);

    window.crypto.getRandomValues(arr);

    for (let i = 0; i < length; i++) {
        password += chars[arr[i] % chars.length]
    }

    return password;
}

```