# git-action-capstone-project
 Automated Pipeline for an E-Commerce Platform. This project entails developing a full-stack application and automating its deployment, offering a comprehensive understanding of Cl/CD practices in a commercial setting. 

## PROJECT SET UP 


#### Create a git repository without initializing it with a README.me file and name it 'e-commerce-platform'
![image](https://github.com/user-attachments/assets/2b5150d1-3936-4685-99f4-5628bfe99282)



#### Clone the repository into local machine 
![image](https://github.com/user-attachments/assets/d6b80b65-f89e-4e8f-a705-579bda94c713)



Change Directory (cd) into the the newly clone repository 
![image](https://github.com/user-attachments/assets/69c36927-33c6-4503-918a-baac281f7771)



#### Inside the repository, create two directories. 'api' for the backend and 'webapp' for the frontend 
![image](https://github.com/user-attachments/assets/aadc4145-1004-4302-a07f-f183ee44f0ba)



#### The project structure should look like this;
![image](https://github.com/user-attachments/assets/2a815fe0-0597-4c6e-a43d-cf4194823481)



#### Create .github/workflows directory in the e-commerce-platform directory
![image](https://github.com/user-attachments/assets/9208e53c-5a0a-41a8-8c0f-26637d1f691b)


# Backend Application set up

## In the 'api' directory, set up a simple Node.js/Express application that handles basic e-commerce operations.

#### cd into the 'api' directory 
![image](https://github.com/user-attachments/assets/489ec50c-d0cd-4d15-8fc9-cf80c1656a0a)


#### Inside the 'api' directory, initialize a new Node.js project by running the following command in the terminal: 'npm init'
![image](https://github.com/user-attachments/assets/4b3d338c-690c-487d-8e88-c918e6151590)


#### Install Express and Mocha (for testing) as dependencies by running: run command 'npm install express mocha chai --save'
![image](https://github.com/user-attachments/assets/e14ef6c7-5171-4ff5-8e6d-91c33138926a)


#### Create a new file named 'server.js' in the 'api' directory and add the following code to set up a basic Express server:
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Welcome to the e-commerce API!');
});

app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});

module.exports = app; // Export the app for testing
![image](https://github.com/user-attachments/assets/340ffb5e-6bfc-4d2f-b18a-217645671889)


#### Create a 'test' directory inside the 'api' directory for unit tests. run command 'mkdir -p test'
![image](https://github.com/user-attachments/assets/22a75fd8-c2fb-4653-9bc8-d59f39cf57dc)


#### In the 'test' directory, create a new file named 'test.js' and add the following sample unit test using Mocha and Chai: run command 'touch test.js'
const chai = require('chai');
const chaiHttp = require('chai-http');
const app = require('../server');

chai.use(chaiHttp);
const expect = chai.expect;

describe('API Endpoint Tests', () => {
  it('should return welcome message on / GET', async () => {
    const res = await chai.request(app).get('/');
    expect(res).to.have.status(200);
    expect(res.text).to.equal('Welcome to the e-commerce API!');
  });
});
![Screenshot 2024-12-05 070501](https://github.com/user-attachments/assets/00417362-f06e-4048-b99a-1e146e64ef55)


#### Update the 'package.json' file to include scripts for running the server and tests:
"scripts": {
  "start": "node server.js",
  "test": "mocha"
}
![Screenshot 2024-12-05 071125](https://github.com/user-attachments/assets/aecca993-526c-4c1a-bbea-ca46efe23c0a)



# Frontend Web Application Setup

## In the 'webapp' directory, create a simple React application that interacts with the backend APl. Ensure the frontend has basic features like
product listing, user login, and order placement.


#### Change directory (cd) into the webapp directory 
![image](https://github.com/user-attachments/assets/08cf952a-13c2-47c8-9c3e-5f41feea56ca)


#### Initialize a new React application by running the following command in the 'webapp' directory: 'npx create-react-app .'
![image](https://github.com/user-attachments/assets/efa99387-7b87-41c5-9ace-941649b9e21b)



####  Install Axios for making API requests by running: 'npm install axios'
![image](https://github.com/user-attachments/assets/e1b2909d-b291-43ef-8ece-1f61f0403787)


## Update the App Component:

#### a. Replace the content of the 'App.js' file with the following code:
import React, { useState } from 'react';
import axios from 'axios';

const App = () => {
  const [products, setProducts] = useState([]);
  const [user, setUser] = useState({});

  const fetchProducts = async () => {
    const response = await axios.get('http://localhost:3000/products'); // Update the URL accordingly
    setProducts(response.data);
  };

  const login = async (username, password) => {
    const response = await axios.post('http://localhost:3000/login', { username, password }); // Update the URL accordingly
    setUser(response.data);
  };

  const placeOrder = async () => {
    const response = await axios.post('http://localhost:3000/order', { user }); // Update the URL accordingly
    // Handle the order placement response
  };

  return (
    <div>
      <h1>E-Commerce Platform</h1>
      <p>Product Listing:</p>
      {products.map(product => (
        <div key={product.id}>
          <h2>{product.name}</h2>
          <p>{product.price}</p>
        </div>
      ))}
      <button onClick={fetchProducts}>Refresh Products</button>

      <p>User Login:</p>
      <input type="text" placeholder="Username" />
      <input type="password" placeholder="Password" />
      <button onClick={() => login(username, password)}>Login</button>

      <p>Place Order:</p>
      <button onClick={placeOrder}>Place Order</button>
    </div>
  );
};

export default App;
#### ![image](https://github.com/user-attachments/assets/33f36757-f63f-4952-b424-ea025d479a2e)


































































































