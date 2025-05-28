from data_structures import Queue
from citizen import Citizen

class Municipality:
    def __init__(self):
        self.waiting_queue = Queue()
        self.citizens = {}  # Dictionary to store citizen objects
    
    def add_citizen(self, name, procedure):
        citizen = Citizen(name, procedure)
        self.waiting_queue.enqueue(citizen)
        if name not in self.citizens:
            self.citizens[name] = citizen
    
    def process_next(self):
        citizen = self.waiting_queue.dequeue()
        if citizen:
            citizen.add_to_history(citizen.procedure)
            return f"Processed: {citizen.name} - {citizen.procedure}"
        return "No citizens in queue."
    
    def display_queue(self):
        queue = self.waiting_queue.display()
        if not queue:
            return "Queue is empty."
        return [f"{citizen.name} - {citizen.procedure}" for citizen in queue]
    
    def get_citizen_history(self, name):
        if name in self.citizens:
            history = self.citizens[name].get_history()
            if not history:
                return f"No history for {name}."
            return [f"{i+1}. {proc}" for i, proc in enumerate(history)]
        return f"Citizen {name} not found."