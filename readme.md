# Library Management API Testing

A comprehensive API testing suite for the Library Management System's Room Service module using Postman with OAuth authentication.

## 📋 Overview

This project contains automated API tests for a Library Management System that manages hotel rooms. The testing suite covers CRUD operations with OAuth authentication and includes both positive and negative test scenarios.

## 🔧 API Endpoints Tested

### Authentication
- **Login**: `POST /login` - Authenticate user and obtain auth code
- **Get Access Token**: `POST /token` - Exchange auth code for access token

### Room Management
- **View Room List**: `GET /viewRoomList` - Retrieve all rooms
- **View Room By ID**: `GET /viewRoomById/{roomId}` - Get specific room details
- **View Room By Type**: `GET /viewRoomByType?roomType={type}` - Filter rooms by type
- **Add Room**: `POST /addRoom` - Create new room
- **Update Room Price**: `PUT /updateRoomPrice` - Modify room pricing
- **Delete Room**: `DELETE /deleteRoomById/{roomId}` - Remove room

## 🚀 Getting Started

### Prerequisites
- Postman installed
- Access to the API endpoints:
  - Auth Service: `https://webapps.tekstac.com/OAuthRestApi/webapi/auth`
  - Room Service: `https://webapps.tekstac.com/HotelAPI/RoomService`

### Environment Variables
Set up the following environment variables in Postman:

```
authUrl: https://webapps.tekstac.com/OAuthRestApi/webapi/auth
baseUrl: https://webapps.tekstac.com/HotelAPI/RoomService
roomId: 101 (or any valid room ID)
roomType: SINGLE (or DOUBLE, SUITE)
authCode: (auto-populated after login)
accessToken: (auto-populated after token request)
```

### Test Credentials
```
Username: user1
Password: pass123
```

## 📊 Test Results Summary

| Test Category | Passed | Failed | Total |
|---------------|--------|---------|-------|
| **Overall** | **17** | **6** | **23** |

### Detailed Test Results

#### ✅ Passing Tests (17)
- **Authentication**: Login and token generation (2 tests)
- **View Operations**: Room list, by ID, by type (9 tests)
- **Data Validation**: Room updates and deletions (6 tests)

#### ❌ Failing Tests (6)
- **Security Tests**: Negative authentication tests for protected endpoints
  - Add Room unauthorized access (2 failures)
  - Update Room unauthorized access (2 failures)
  - Delete Room unauthorized access (2 failures)

## 🧪 Test Categories

### 1. Authentication Tests
- **Login**: Validates user credentials and captures auth code
- **Token Exchange**: Converts auth code to access token

### 2. Read Operations
- **Room List**: Verifies API returns complete room inventory
- **Room by ID**: Tests specific room retrieval with ID validation
- **Room by Type**: Filters rooms by type (SINGLE, DOUBLE, SUITE)

### 3. Write Operations
- **Add Room**: Creates new room entries
- **Update Room Price**: Modifies existing room pricing
- **Delete Room**: Removes rooms from inventory

### 4. Security Tests (Negative Testing)
- Tests unauthorized access to protected endpoints
- Validates proper authentication enforcement

## 📈 Performance Metrics

- **Total Execution Time**: 721ms
- **Average Response Time**: 90ms per request
- **Fastest Response**: 43ms (View Room List)
- **Slowest Response**: 327ms (Login)

## 🔍 Test Implementation Details

### Automated Validations
- HTTP status code verification
- Response format validation (JSON)
- Data integrity checks
- Business logic validation
- Security compliance testing

### Test Data Management
- Dynamic variable capture and reuse
- Environment-based configuration
- Automated cleanup procedures

## 🏗️ Collection Structure

```
Library_Management_API_Testing/
├── Authentication/
│   ├── Login
│   └── Get Access Token
└── Room Management/
    ├── View Room List
    ├── View Room By ID
    ├── View Room By Type
    ├── Add Room
    ├── Update Room Price
    └── Delete Room by ID
```

## 🔧 Usage Instructions

### Step 1: Install Postman

#### 1.1 Download Postman
1. **Visit the official website**: Go to [https://www.postman.com/downloads/](https://www.postman.com/downloads/)
2. **Select your operating system**: The website should automatically detect your OS (Windows, Mac, or Linux)
3. **Choose version**: Select the appropriate version:
   - **Windows**: Download `.exe` file
   - **Mac

### Step 2: Import the Collection
1. **Open Postman** and click on **"Import"** button (top-left corner)
2. **Select File**: Choose `Sprint3_Collection.json` from your local directory
3. **Import Options**: Keep default settings and click **"Import"**
4. **Verify Import**: You should see "Library_Management_API_Testing" in your Collections panel

### Step 3: Create Environment
1. **Click Environment Tab**: Located in left sidebar
2. **Create New Environment**: Click **"+"** or **"Create Environment"**
3. **Name Environment**: Enter `Library_Management_Test_Env`
4. **Add Variables**: Create the following variables with their values:

| Variable Name | Initial Value | Current Value |
|---------------|---------------|---------------|
| `authUrl` | `https://webapps.tekstac.com/OAuthRestApi/webapi/auth` | `https://webapps.tekstac.com/OAuthRestApi/webapi/auth` |
| `baseUrl` | `https://webapps.tekstac.com/HotelAPI/RoomService` | `https://webapps.tekstac.com/HotelAPI/RoomService` |
| `roomId` | `101` | `101` |
| `roomType` | `SINGLE` | `SINGLE` |
| `authCode` | *(leave empty)* | *(leave empty)* |
| `accessToken` | *(leave empty)* | *(leave empty)* |

5. **Save Environment**: Click **"Save"** button

### Step 4: Select Environment
1. **Environment Dropdown**: Click dropdown in top-right corner of Postman
2. **Select Environment**: Choose `Library_Management_Test_Env`
3. **Verify Selection**: Environment name should appear in dropdown

### Step 5: Run Complete Test Suite
1. **Open Collection**: Click on "Library_Management_API_Testing" collection
2. **Run Collection**: Click **"Run"** button (or three dots → Run collection)
3. **Collection Runner**: 
   - Select all requests (default)
   - Set iterations: `1`
   - Set delay: `0ms` (or 1000ms for slower execution)
4. **Start Run**: Click **"Run Library_Management_API_Testing"**
5. **Monitor Progress**: Watch tests execute in real-time

### Step 6: Running Individual Tests

#### Option A: Sequential Execution (Recommended)
**Important**: Always run authentication first, then other tests

1. **Run Login First**:
   ```
   POST {{authUrl}}/login
   ```
   - Opens "Login" request
   - Click **"Send"**
   - Verify response status: `200 OK`
   - Check authCode is captured in environment

2. **Get Access Token**:
   ```
   POST {{authUrl}}/token
   ```
   - Click **"Send"**
   - Verify response status: `200 OK`
   - Check accessToken is captured in environment

3. **Run Room Operations**:
   ```
   GET {{baseUrl}}/viewRoomList
   GET {{baseUrl}}/viewRoomById/{{roomId}}
   GET {{baseUrl}}/viewRoomByType?roomType={{roomType}}
   ```

#### Option B: Individual Request Testing
1. **Select Request**: Click on any request in collection
2. **Review Parameters**: Check URL, headers, and body
3. **Send Request**: Click **"Send"** button
4. **Analyze Response**: Review status, headers, and body
5. **Check Tests**: View test results in **"Test Results"** tab

### Step 7: Understanding Test Results

#### Test Results Panel
- **Green ✓**: Test passed
- **Red ✗**: Test failed
- **Test Name**: Description of what was tested
- **Error Details**: Click on failed test to see details

#### Console Logs
1. **Open Console**: Click **"Console"** at bottom of Postman
2. **View Logs**: See detailed execution information
3. **Debug Issues**: Use console.log() outputs for troubleshooting

### Step 8: Customizing Tests

#### Modify Test Data
1. **Edit Room ID**: Change `roomId` environment variable
2. **Change Room Type**: Update `roomType` variable (SINGLE, DOUBLE, SUITE)
3. **Update Credentials**: Modify login body if needed

#### Add New Room Test
```javascript
// Example: Test adding a new room
POST {{baseUrl}}/addRoom
Body (x-www-form-urlencoded):
roomId: 999
hotelId: H2001
roomType: DOUBLE
roomStatus: AVAILABLE
roomPrice: 2000
```

### Step 9: Troubleshooting

#### Common Issues & Solutions

**Issue 1**: Authentication failures
```
Solution: 
1. Verify credentials (user1/pass123)
2. Check authUrl is correct
3. Ensure environment is selected
```

**Issue 2**: Environment variables not working
```
Solution:
1. Verify environment is selected (top-right dropdown)
2. Check variable names match exactly
3. Ensure variables are saved
```

**Issue 3**: Tests failing due to data dependencies
```
Solution:
1. Run Login → Get Token → Other tests in sequence
2. Verify roomId exists in system
3. Check if test data was modified by previous tests
```

### Step 10: Advanced Usage

#### Running with Newman (CLI)
1. **Install Newman**:
   ```bash
   npm install -g newman
   ```

2. **Export Collection & Environment**:
   - Collection: Export as `collection.json`
   - Environment: Export as `environment.json`

3. **Run via Command Line**:
   ```bash
   newman run collection.json -e environment.json --reporters html
   ```

#### Automated Testing with CI/CD
```yaml
# Example GitHub Actions workflow
- name: Run API Tests
  run: |
    newman run Sprint3_Collection.json \
    -e test_environment.json \
    --reporters junit,html \
    --reporter-junit-export results.xml
```

### Step 11: Best Practices

1. **Always authenticate first** before running protected endpoints
2. **Use unique test data** to avoid conflicts
3. **Clean up test data** after test execution
4. **Monitor response times** for performance issues
5. **Review failed tests** to identify API issues
6. **Keep environment variables updated** with current values

### Step 12: Expected Test Outcomes

#### Successful Execution Should Show:
- ✅ 17 passed tests
- ❌ 6 failed tests (expected - security testing)
- Total execution time: ~721ms
- All GET operations return 200 status
- Authentication flow completes successfully

## 📋 Test Scenarios

### Positive Test Cases
- ✅ Successful authentication flow
- ✅ Retrieve room data with valid parameters
- ✅ CRUD operations with proper authorization
- ✅ Data format and structure validation

### Negative Test Cases
- ❌ Unauthorized access to protected endpoints
- ✅ Invalid parameter handling
- ✅ Data integrity validation

## 🐛 Known Issues

1. **Authentication Bypass**: Some protected endpoints are accessible without proper authorization
2. **Security Gap**: Negative authentication tests are failing, indicating potential security vulnerabilities

## 📝 Notes

- The API appears to have authentication mechanisms but may not be enforcing them consistently
- Consider implementing stricter authorization checks for write operations
- Test execution shows good performance with sub-second response times
- Data validation tests are comprehensive and passing

## 🔄 Continuous Integration

This collection can be integrated with:
- Newman (Postman CLI)
- Jenkins/GitHub Actions
- Automated testing pipelines

## 📞 Support

For issues or questions regarding the API testing suite, please refer to the project documentation or contact the development team.