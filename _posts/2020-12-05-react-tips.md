# intercept requests or responses

```
import React, {useEffect} from "react";
import axios from "axios";

const checkRequests= Wrapped => {
    function CheckRequests(props) {
        useEffect(()=>{
            axios.interceptors.response.use(function (response) {
                // Do something with response data
                return response;
            }, function (error) {
                switch (error.response.status) {
                    case 503 :
                        props.history.push('/503') //we will redirect user into 503 page 
                        break
                    default :
                        break
                }
                // Do something with response error
                return Promise.reject(error);
            });
        })

        return (
            <Wrapped {...props} />
        )
    }
    return CheckRequests
}

export default checkRequests
```

# loading-indicator
```
.loading-indicator:before {
    content: '';
    background: #000000cc;
    position: fixed;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    z-index: 1000;
}

.loading-indicator:after {
    content: 'Loading';
    position: fixed;
    width: 100%;
    top: 50%;
    left: 0;
    z-index: 1001;
    color:white;
    text-align:center;
    font-weight:bold;
    font-size:1.5rem;        
}
```
```
Axios.interceptors.request.use(function (config) {

  // spinning start to show
  // UPDATE: Add this code to show global loading indicator
  document.body.classList.add('loading-indicator');

  const token = window.localStorage.token;
  if (token) {
     config.headers.Authorization = `token ${token}`
  }
  return config
}, function (error) {
  return Promise.reject(error);
});

Axios.interceptors.response.use(function (response) {

  // spinning hide
  // UPDATE: Add this code to hide global loading indicator
  document.body.classList.remove('loading-indicator');

  return response;
}, function (error) {
  return Promise.reject(error);
});
```