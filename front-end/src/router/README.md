# src/router
🧱 Basic Structure Example
plaintext
Copy code
src/
├── router/
│   ├── AppRouter.jsx           ← main routing setup
│   ├── PrivateRoute.jsx        ← wrapper for authenticated routes
│   └── AdminRoute.jsx          ← wrapper for admin-only routes (optional)
📌 Example: AppRouter.jsx
jsx
Copy code
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import HomePage from '../pages/HomePage';
import LoginPage from '../pages/LoginPage';
import RegisterPage from '../pages/RegisterPage';
import CourseListPage from '../pages/CourseListPage';
import CourseDetailPage from '../pages/CourseDetailPage';
import DashboardPage from '../pages/DashboardPage';
import NotFoundPage from '../pages/NotFoundPage';
import PrivateRoute from './PrivateRoute';

const AppRouter = () => {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<HomePage />} />
        <Route path="/login" element={<LoginPage />} />
        <Route path="/register" element={<RegisterPage />} />
        
        <Route path="/courses" element={<CourseListPage />} />
        <Route path="/courses/:id" element={<CourseDetailPage />} />

        {/* Protected route */}
        <Route
          path="/dashboard"
          element={
            <PrivateRoute>
              <DashboardPage />
            </PrivateRoute>
          }
        />

        {/* 404 */}
        <Route path="*" element={<NotFoundPage />} />
      </Routes>
    </BrowserRouter>
  );
};

export default AppRouter;
🔐 Example: PrivateRoute.jsx
jsx
Copy code
import React from 'react';
import { Navigate } from 'react-router-dom';
import { useSelector } from 'react-redux';

const PrivateRoute = ({ children }) => {
  const user = useSelector((state) => state.auth.user);
  return user ? children : <Navigate to="/login" replace />;
};

export default PrivateRoute;
🔐 (Optional) AdminRoute.jsx
jsx
Copy code
const AdminRoute = ({ children }) => {
  const { user } = useSelector((state) => state.auth);
  const isAdmin = user?.role === 'admin';
  return isAdmin ? children : <Navigate to="/unauthorized" replace />;
};
🧠 Pro Tips
Avoid putting all routes inside App.jsx — use AppRouter.jsx

Keep paths as constants (like ROUTES.js) for reuse

Protect private/admin routes using wrappers

Create dynamic routes like /courses/:id, /quiz/:quizId

🗂 Bonus: Route Path Constants (Optional)
Create src/constants/routes.js:

js
Copy code
export const ROUTES = {
  HOME: '/',
  LOGIN: '/login',
  REGISTER: '/register',
  COURSES: '/courses',
  COURSE_DETAIL: (id) => `/courses/${id}`,
  DASHBOARD: '/dashboard',
};
Then in components:

js
Copy code
<Link to={ROUTES.COURSES}>Browse Courses</Link>