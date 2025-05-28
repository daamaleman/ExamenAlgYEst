from data_structures import Stack

class Citizen:
    def __init__(self, name, procedure):
        self.name = name
        self.procedure = procedure
        self.history = Stack()  # Stack for individual procedure history
    
    def add_to_history(self, procedure):
        self.history.push(procedure)
    
    def get_history(self):
        history = []
        temp_stack = Stack()
        
        # Copy history to temporary stack to preserve order
        while not self.history.is_empty():
            item = self.history.pop()
            history.append(item)
            temp_stack.push(item)
        
        # Restore history to original stack
        while not temp_stack.is_empty():
            self.history.push(temp_stack.pop())
        
        return history[::-1]  # Return reversed for chronological order