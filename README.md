# Flexiplan
Automated Task Scheduling System

# Intelligent Task Scheduling System Using Constraint Programming

## 1. Introduction

The Intelligent Task Scheduling System is an advanced project management solution that leverages Constraint Satisfaction Programming (CSP) through Google's OR-Tools to optimize task assignments in organizations. This system addresses the complex challenge of matching employees with projects based on skills, time constraints, and workload distribution.

### Problem Statement
Modern organizations face several challenges in project management:
- Efficiently matching employee skills with project requirements
- Managing employee workload and avoiding overallocation
- Meeting project deadlines while maintaining work quality
- Optimizing resource utilization across multiple projects
- Ensuring fair distribution of work among team members

## 2. Proposed Solution

Our solution implements a sophisticated task scheduling system using constraint programming to optimize project assignments.

### 2.1 System Architecture

The system is built on three primary classes:

1. **Employee Class**
```python
class Employee:
    def __init__(self, name, skills, daily_hours):
        self.name = name
        self.skills = skills
        self.daily_hours = daily_hours
        self.remaining_hours = daily_hours
```

2. **Project Class**
```python
class Project:
    def __init__(self, title, required_skills, hours_needed, deadline):
        self.title = title
        self.required_skills = required_skills
        self.hours_needed = hours_needed
        self.deadline = deadline
```

3. **TaskScheduler Class**
- Core scheduling logic implementation
- Constraint satisfaction solver integration
- Resource management and assignment tracking

### 2.2 Key Features

1. **Skill-Based Assignment**
   - Matches employee skills with project requirements
   - Ensures qualified resource allocation
   - Supports multiple skills per employee

2. **Workload Management**
   - Tracks daily available hours
   - Prevents resource overallocation
   - Maintains work-hour balance

3. **Constraint Programming Integration**
   - Uses Google OR-Tools for optimization
   - Implements complex scheduling constraints
   - Provides optimal assignment solutions

### 2.3 Technical Implementation

#### Constraint Model Setup
```python
def schedule_tasks(self):
    model = cp_model.CpModel()
    assignments = {}
    for project in self.projects:
        assignments[project.title] = [
            model.NewBoolVar(f"{project.title}_{employee.name}")
            for employee in self.employees
        ]
```

#### Core Constraints
1. **Single Assignment Constraint**
```python
model.Add(sum(assignments[project.title]) == 1)
```

2. **Skill Matching Constraint**
```python
model.AddBoolOr([
    assignments[project.title][j].Not()
] + [
    skill.lower() in [s.lower() for s in employee.skills]
    for skill in project.required_skills
])
```

3. **Workload Constraint**
```python
model.Add(
    assignments[project.title][j] * project.hours_needed
    <= employee.remaining_hours
)
```

### 2.4 Algorithm Design

The scheduling algorithm follows a three-step process:

1. **Initialization Phase**
   - Create constraint model
   - Define assignment variables
   - Set up basic constraints

2. **Constraint Application**
   - Apply skill matching rules
   - Implement workload restrictions
   - Add deadline constraints

3. **Optimization**
   - Minimize total remaining hours
   - Balance workload distribution
   - Find optimal assignment solution

## 3. Results and Analysis

### 3.1 System Performance

The implementation demonstrates several key capabilities:

1. **Assignment Accuracy**
   - Successfully matches skills to requirements
   - Maintains workload balance
   - Respects time constraints

2. **Resource Utilization**
   - Optimizes employee availability
   - Prevents skill mismatches
   - Maximizes productivity

3. **Constraint Satisfaction**
   - Enforces all defined constraints
   - Provides feasible solutions
   - Handles complex scenarios

### 3.2 User Interface

The system provides an interactive command-line interface with the following options:
1. Add Employee
2. Add Project
3. Schedule Tasks
4. View Assignments
5. Exit

### 3.3 Limitations and Future Improvements

Current limitations:
- Fixed daily hours constraint
- Basic deadline handling
- Limited priority support

Potential improvements:
- GUI implementation
- Advanced scheduling algorithms
- Priority-based scheduling
- Dynamic workload adjustment
- Multi-period planning support

## 4. Technical Requirements

### Dependencies
```
pandas
ortools
datetime
```

### Installation
```bash
pip install pandas ortools openpyxl
```

### System Requirements
- Python 3.7+
- Sufficient memory for constraint solving
- Compatible operating system

## 5. Conclusion

The Intelligent Task Scheduling System successfully demonstrates the application of constraint programming in solving complex resource allocation problems. The system provides an efficient, automated approach to project scheduling while ensuring optimal resource utilization and workload balance.

Key achievements:
- Successful implementation of constraint-based scheduling
- Efficient skill-project matching
- Automated workload optimization
- Scalable solution for project management

The modular design and use of advanced optimization techniques make this system a valuable tool for modern project management needs.
