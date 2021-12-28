# integration-testing-with-postman

**Integration test with Postman and Javascript for API used in comment process in Çiçeksepeti**

**GET**  ```https://www.getpostman.com/collections/c0a484250e8d7efbafa0```

## Step 1

First step, we'll import the Postman collection into Postman.

#### Instructions

- Open Postman

- Click on the  ```import``` button located in the top left corner of Postman

- The file you are importing is inside of the ```postman_collection``` folder in this repo

- After importing, you should have a collection called ```Ciceksepeti Bootcamp```

## Step 2

#### Instructions

In this step, we will create a Postman test to fetching the return response on the city name value.

- Click on the ```GET-Comment by City Name``` request

- Click on the ```Send``` button to see the returned data

- Create tests to check the returned ```cityName``` values


> **Create a test to the test fails when there are no 4 items in the returned response**

```javascript
const actualResponse = pm.response.json();
const itemLength = actualResponse.item.length;

pm.test("Response Control Item Size " ,() => {
    if(itemLength !== 4){
        console.log("TEST FAİLED");
    }
});
```

> **Create a test to verify the returned for Ankara and İstanbul list of comments**

```javascript
pm.test("Response Control for City Name Value: " + requestValue ,() => {
if(requestKey==="cityName" && requestValue ==="ankara" || requestValue==="istanbul"){
    pm.expect(responseKey).to.eql(requestKey);
    pm.expect(responseValue).to.eql(requestValue); 
    pm.expect(responseCode).to.eql(200);
    pm.expect(responseBody).to.include("reviewDtos").to.include("comment");
}
});
```

> **Create a test to verify the returned for not found Van**

```javascript
pm.test("Response Control for City Name Value: " + requestValue ,() => {
if(requestKey==="cityName" && requestValue ==="van"){
    pm.expect(responseKey).to.eql(requestKey);
    pm.expect(responseValue).to.eql(requestValue); 
    pm.expect(responseStatus).to.eql("Not Found");
    pm.expect(responseCode).to.eql(404);
    pm.expect(responseBody).to.contain("Not Found");
}
});
```

> **Create a test to verify the returned null city name**

```javascript
pm.test("Response Control for City Name Value: " + requestValue ,() => {
if(requestKey==="cityName" && requestValue ===""){
    pm.expect(responseKey).to.eql(requestKey);
    pm.expect(responseValue).to.eql(requestValue); 
    pm.expect(responseStatus).to.eql("Bad Request");
    pm.expect(responseCode).to.eql(400);
    pm.expect(responseBody).to.contain("'cityName' can not be null.");
}
});
```

![image](https://user-images.githubusercontent.com/55894683/147583625-c7a7ff0d-6f1c-4dc0-b01f-14fdc8ac4512.png)



