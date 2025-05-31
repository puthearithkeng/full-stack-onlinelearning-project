# src/services
Put API logic here:

Separate file for each feature's backend API (authAPI.js, courseAPI.js, etc.)

Example:

js
Copy code
// authAPI.js
import axios from 'axios';
export const login = (credentials) => axios.post('/api/user/login', credentials);
