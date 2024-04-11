
#### 1. Self-Review the Code When MR Is Created
- **Example Swift Code Review:**
  ```swift
  // Before review: Violates single responsibility principle
  func fetchDataAndUpdateUI() {
      // Fetch data and update UI
  }

  // After self-review: Separated concerns
  func fetchData() -> Data {
      // Fetch data
  }
  func updateUI(data: Data) {
      // Update UI
  }
  ```

#### 2. Add Desired Comments and Reason for Particular Code
- **Example Explanation Comment:**
  ```swift
  // Chose bubble sort for its simplicity and because our data set is always small (n < 10)
  func bubbleSort(_ array: [Int]) -> [Int] {
      // Sorting logic
  }
  ```

#### 3. Mention Your Ticket IDs and Reason for Everything
- **Example MR Description:**
  ```
  // Implements caching as per Ticket #1234 to reduce API calls
  func cacheData(data: Data) {
      // Cache data
  }
  ```

#### 4. If You Are Going to Refactor Code in Future Just Add the Comment
- **Example TODO Comment:**
  ```swift
  // TODO: Refactor this method to split JSON parsing and data fetching (Ticket #5678)
  func fetchData() {
      // Fetch and parse data
  }
  ```

#### 5. If You Found Out That There Is Some Problem in Code Fix It Instantly After Seeing It in Comparison of Code
- **Example Immediate Fix:**
  ```swift
  // Before: Risk of retain cycle
  networkManager.fetchData { [unowned self] data in
      self.updateUI(data: data)
  }

  // After: Fixed retain cycle risk
  networkManager.fetchData { [weak self] data in
      self?.updateUI(data: data)
  }
  ```


#### 6. Use Meaningful Variable and Function Names
- **Example:**
  ```swift
  // Poor naming
  func d(_ d: Data) {
      // Process data
  }

  // Improved naming
  func processData(_ data: Data) {
      // Process data
  }
  ```

#### 7. Avoid Force Unwrapping and Use Optional Binding
- **Example:**
  ```swift
  // Before: Force unwrapping
  let name: String = dictionary["name"]!

  // After: Optional binding
  if let name = dictionary["name"] as? String {
      // Use name
  }
  ```

#### 8. Prefer High-Order Functions Over Loops
- **Example:**
  ```swift
  // Before: Looping
  var doubledNumbers = [Int]()
  for number in numbers {
      doubledNumbers.append(number * 2)
  }

  // After: Using map
  let doubledNumbers = numbers.map { $0 * 2 }
  ```

#### 9. Leverage Swift’s Type System for Safety
- **Example:**
  ```swift
  // Before: Less type-safe
  func calculateArea(width: Float, height: Float) -> Float {
      return width * height
  }

  // After: More type-safe
  struct Size {
      let width: Float
      let height: Float
  }
  func calculateArea(size: Size) -> Float {
      return size.width * size.height
  }
  ```

#### 10. Use Guard Statements for Early Exits
- **Example:**
  ```swift
  // Before: Nested if
  func updateProfile(with dictionary: [String: Any]) {
      if let name = dictionary["name"] as? String {
          // Update profile
      }
  }

  // After: Guard statement
  func updateProfile(with dictionary: [String: Any]) {
      guard let name = dictionary["name"] as? String else { return }
      // Update profile
  }
  ```

#### 11. Write Self-Documenting Code
- **Example:**
  ```swift
  // Instead of adding a comment, make the code clear
  let elapsedTimeInSeconds = 120 // Better than just 'elapsedTime'
  ```

#### 12. Keep Functions Short and Focused
- **Example:**
  ```swift
  // Before: Multiple responsibilities
  func handleUserInput() {
      // Validate input, save data, and update UI
  }

  // After: Single responsibility
  func validateUserInput() {
      // Validate input
  }
  func saveUserData() {
      // Save data
  }
  func updateUI()

 {
      // Update UI
  }
  ```

#### 13. Optimize for Readability Over Cleverness
- **Example:**
  ```swift
  // Before: Hard to read
  let result = numbers.filter{$0 > 50}.map{$0 * 2}.reduce(0, +)

  // After: Easier to understand
  let filteredNumbers = numbers.filter { $0 > 50 }
  let doubledNumbers = filteredNumbers.map { $0 * 2 }
  let result = doubledNumbers.reduce(0, +)
  ```

#### 14. Use Enums for State and Option Management
- **Example:**
  ```swift
  // Before: Using strings for states
  let status = "loading"

  // After: Using enum
  enum Status {
      case loading
      case success
      case error
  }
  let status: Status = .loading
  ```

#### 15. Regularly Refactor Legacy Code During Feature Development
- **Example:**
  ```swift
  // While adding a new feature, improve the surrounding code
  // TODO: Refactor this old parsing method to use Codable (Ticket #91011)
  func parseData() {
      // Parse data
  }
  ```

Incorporating these practices into your code review process can significantly improve the maintainability, readability, and overall quality of your Swift codebase, fostering a culture of excellence in your iOS development team.