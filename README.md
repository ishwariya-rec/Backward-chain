# Backward-chain
# backward_chaining.py

def backward_chaining(rules, facts, goal, visited=None):
    if visited is None:
        visited = set()

  if goal in facts:
        return True

  if goal in visited:
        return False  # Prevent infinite loops

  visited.add(goal)

  for rule in rules:
        head, body = rule
        if head == goal:
            if all(backward_chaining(rules, facts, subgoal, visited) for subgoal in body):
                facts.append(goal)
                return True

  return False

# --------- Knowledge Base ---------
rules = [
    ("cold", ["rainy"]),
    ("wear_jacket", ["cold"]),
    ("wet", ["rainy"]),
    ("rainy", ["cloudy", "humid"]),
    ("humid", ["summer"])
]

facts = ["cloudy", "summer"]

# --------- Query ---------
goal = "wear_jacket"
result = backward_chaining(rules, facts, goal)

print(f"Can we infer '{goal}'? {'Yes' if result else 'No'}")
