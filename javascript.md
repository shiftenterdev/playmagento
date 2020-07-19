## API

**Fetch (get)**
> Native ajax alternative call
```javascript
// Json output
fetch('http://website.com/api')
    .then(response => response.json())
    .then(r => {
        console.log(r);
    });

// Text output
fetch('http://website.com/api')
    .then(response => response.text())
    .then(r => {
        console.log(r);
    });
```

**Fetch (post)**
```javascript
fetch('/business', {
        method: 'post',
        credentials: "same-origin",
        headers: {
            'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
        },
        body: new FormData(document.getElementById('businessForm'))
    })
        .then(r => r.json())
        .then(r => {
            console.log(r);
        })
```
?> For header you can also use a helper object like
```javascript
async function postData(url = '', data = {}) {
        // Default options are marked with *
        const response = await fetch(url, {
            method: 'POST', // *GET, POST, PUT, DELETE, etc.
            mode: 'cors', // no-cors, *cors, same-origin
            cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
            credentials: 'same-origin', // include, *same-origin, omit
            headers: {
                'Content-Type': 'application/json',
                'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
                // 'Content-Type': 'application/x-www-form-urlencoded',
            },
            redirect: 'follow', // manual, *follow, error
            referrerPolicy: 'no-referrer', // no-referrer, *no-referrer-when-downgrade, origin, origin-when-cross-origin, same-origin, strict-origin, strict-origin-when-cross-origin, unsafe-url
            body: JSON.stringify(data) // body data type must match "Content-Type" header
        });
        return response.json(); // parses JSON response into native JavaScript objects
    }
```
?> Then your request will be
```javascript
fetch('/business', postData('/business',{name:name,age:age}))
        .then(r => r.json())
        .then(r => {
            console.log(r);
        })
```

## Helper function
> Check file extension
```javascript
var fExt = $(this).val().split('.').pop().toLowerCase();
if($.inArray(fExt, ['jpg','jpeg']) == -1) {
    alert('invalid extension!');
    return false;
}
```

