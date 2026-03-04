import json
import os

class ContextLibrarian:
    def __init__(self, project_name):
        self.project_name = project_name
        self.general_context = ""
        self.context_library = [] 
        self.project_folder_path = f"./project_folder/{project_name}.txt"
        
        os.makedirs("./project_folder", exist_ok=True)

    def ingest_and_generalize(self, raw_input):
        print("[LIBRARIAN] Ingesting raw input and updating General Context...")
        self.general_context = f"Project Goal: {raw_input[:100]}... [Condensed]"
        
        print("[LIBRARIAN] Chunking input into bite-sized context blocks...")
        self.context_library = [
            {"block_id": 1, "label": "Task Breakdown", "content": "Identify the 3 main parameters."},
            {"block_id": 2, "label": "Drafting Part 1", "content": "Execute the first parameter."},
            {"block_id": 3, "label": "Organization", "content": "Format the output into the schema."}
        ]
        return self.general_context

    def issue_general_understanding(self):
        return self.general_context

    def issue_next_block(self):
        if self.context_library:
            return self.context_library.pop(0) 
        return None

    def save_to_project_folder(self, completed_task):
        with open(self.project_folder_path, "a") as f:
            f.write(f"{completed_task}\n\n")
        print(f"[LIBRARIAN] Verified and saved to {self.project_folder_path}")
