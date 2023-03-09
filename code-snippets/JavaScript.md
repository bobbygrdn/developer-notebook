# Code Snippets

## Table of Contents

### Generate Password Function

```javascript
const generatePassword = () => {
  let password = "";
  let length = 16;

  const chars = `0123456789abcdefghijklmnopqrstuvwxyz!@#$%^&*()ABCDEFGHIJKLMNOPQRSTUVWXYZ`;

  const arr = new Uint32Array(length);

  window.crypto.getRandomValues(arr);

  for (let i = 0; i < length; i++) {
    password += chars[arr[i] % chars.length];
  }

  return password;
};
```

### GR Code Generator

```javascript
const generateGR() {
    document.querySelector('#gr-image').style.display = "block";
    let QRtext = document.querySelector('#text');
    if(GRtext.trim().length == 0) {
        document.querySelector('#qr-image .error').innerHTML = "Please enter text";
        document.querySelector('#img').style.display = "none";
    } else {
        document.querySelector('#img').style.display = "block";
        document.querySelector('#qr-image .error').innerHTML = "";
        document.querySelector('#img').src = "https://api.qrserver.com/v1/create-qr-code/?size=240x240&data=" + QRtext;
    }
}
```
