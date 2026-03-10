# ExpNo:10 Implementation of Classical Planning Algorithm

NAME:  JAYANI N
REG NO: 212224100025


# Algorithm or Steps Involved:
<ol>
  <li>Define the initial state</li>
  <li>Define the goal state</li>
  <li>Define the actions</li>
  <li>Find a <b>plan</b> to reach the goal state</li>
  <li>Print the plan</li>
</ol>

# Example - 1
```
initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B']
```
# Example - 2
```
initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```


## PROGRAM:



    def is_goal_state(current_state, goal_state):
        # Check if all keys in goal_state match the current_state
        return all(current_state.get(k) == v for k, v in goal_state.items())
    
    def apply_action(current_state, action_effect):
        new_state = current_state.copy()
        new_state.update(action_effect)
        return new_state
    
    def is_applicable(current_state, precondition):
        # Check if all preconditions are satisfied in the current state
        return all(current_state.get(k) == v for k, v in precondition.items())
    
    def find_plan(initial_state, goal_state, actions):
        # Breadth-first search for plan
        queue = [(initial_state, [])]  # Each element is (state, plan_so_far)
        visited_states = set()
    
        while queue:
            current_state, partial_plan = queue.pop(0)
    
            # Check if goal reached
            if is_goal_state(current_state, goal_state):
                return partial_plan
    
            # Avoid revisiting states
            state_tuple = tuple(sorted(current_state.items()))
            if state_tuple in visited_states:
                continue
            visited_states.add(state_tuple)
    
            # Explore all applicable actions
            for action_name, action_data in actions.items():
                if is_applicable(current_state, action_data['precondition']):
                    next_state = apply_action(current_state, action_data['effect'])
                    queue.append((next_state, partial_plan + [action_name]))
    
        print("No plan exists.")
        return None
    
    # ---------------- Example 1 ----------------
    initial_state = {'A': 'Table', 'B': 'Table'}
    goal_state = {'A': 'B', 'B': 'Table'}
    
    actions = {
        'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
        'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
    }
    
    plan = find_plan(initial_state, goal_state, actions)
    print("Example 1 Plan:", plan)
    
    # ---------------- Example 2 ----------------
    initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
    goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}
    
    actions = {
        'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
        'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
        'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
    }
    
    plan = find_plan(initial_state, goal_state, actions)
    print("Example 2 Plan:", plan)


# Output:


<img width="700" height="258" alt="image" src="https://github.com/user-attachments/assets/ff2d48fc-5623-47ba-ad60-d0779ce71fe6" />



