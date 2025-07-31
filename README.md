# Job Application Priority Queue System

This system provides an efficient way for hiring teams to manage and evaluate job applicants based on their qualifications.

## Overview

This Java program implements a priority queue system for managing job applications. It evaluates candidates based on their scores and maintains applications in a min-heap structure to efficiently track the highest-scoring applicants for open positions.

## Key Components

### 1. Application Class
- Models a job application with name, email, and score (0-100)
- Implements `Comparable` to enable comparison based on scores
- Includes validation for all fields
- Provides getter methods and a formatted string representation

### 2. ApplicationQueue Class
- Array-based min-heap implementation of a priority queue
- Maintains applications in order from lowest to highest score
- Core operations:
  - `enqueue()` - Adds new applications while maintaining heap structure
  - `dequeue()` - Removes and returns the lowest-scoring application
  - `peek()` - Views the lowest-scoring application without removal
- Supports iteration through applications in score order

### 3. OpenPosition Class
- Manages applications for a specific job opening
- Only retains the highest-scoring applicants up to the position's capacity
- Provides methods to:
  - Add new applications (replacing lower scores when full)
  - View current applications
  - Calculate total score of all current applicants

### 4. ApplicationIterator Class
- Provides iteration capability for ApplicationQueue
- Returns applications in order from lowest to highest score
- Creates a deep copy of the queue to avoid modifying the original data

## How It Works

1. **Application Submission**:
   - Applications are created with validated name, email, and score
   - Applications are added to an OpenPosition's priority queue

2. **Priority Queue Management**:
   - The queue automatically maintains applications in min-heap order
   - When capacity is reached, new applications only replace existing ones if they have higher scores

3. **Application Review**:
   - Hiring managers can view all applications in score order
   - The system provides the total score of all current applicants

## Testing

The `OpenPositionTester` class includes comprehensive unit tests for:
- Application validation and comparison
- Priority queue operations (enqueue/dequeue)
- Iterator functionality
- OpenPosition management features

## Usage Example

```java
// Create an open position with capacity for 3 applicants
OpenPosition developerPosition = new OpenPosition("Software Developer", 3);

// Add applications
developerPosition.add(new Application("Alice", "alice@email.com", 85));
developerPosition.add(new Application("Bob", "bob@email.com", 92));
developerPosition.add(new Application("Charlie", "charlie@email.com", 78));

// Try to add another application (will only be added if score is high enough)
developerPosition.add(new Application("Dana", "dana@email.com", 95));

// View current applications
System.out.println(developerPosition.getApplications());

// Get total score
System.out.println("Total score: " + developerPosition.getTotalScore());
```

## Design Considerations

- **Min-Heap Structure**: Ensures efficient O(log n) operations for adding/removing applications
- **Capacity Management**: Automatically maintains only the highest-scoring applicants
- **Immutable Applications**: Once created, application data cannot be modified
- **Deep Copying**: Prevents unintended modification of queue data during iteration
