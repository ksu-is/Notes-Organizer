import datetime

class Note:
    def __init__(self, title, content, topic):
        self.title = title
        self.content = content
        self.topic = topic
        self.date_created = datetime.datetime.now()

    def __str__(self):
        return f"Title: {self.title}\nTopic: {self.topic}\nDate: {self.date_created.strftime('%Y-%m-%d %H:%M:%S')}\nContent: {self.content}\n"

class NotesOrganizer:
    def __init__(self):
        self.notes = []

    def add_note(self, title, content, topic):
        new_note = Note(title, content, topic)
        self.notes.append(new_note)
        print("Note added successfully!")

    def view_notes(self):
        if not self.notes:
            print("No notes available.")
            return
        for idx, note in enumerate(self.notes, start=1):
            print(f"\n--- Note {idx} ---")
            print(note)

    def sort_notes(self, criterion):
        if criterion == "alphabetical":
            self.notes.sort(key=lambda x: x.title.lower())
        elif criterion == "topic":
            self.notes.sort(key=lambda x: x.topic.lower())
        elif criterion == "date":
            self.notes.sort(key=lambda x: x.date_created)
        else:
            print("Invalid sort criterion.")
            return
        print(f"Notes sorted by {criterion}.")

    def delete_note(self, title):
        for note in self.notes:
            if note.title.lower() == title.lower():
                self.notes.remove(note)
                print(f"Note titled '{title}' deleted successfully.")
                return
        print(f"No note found with the title '{title}'.")

# Main Functionality
def main():
    organizer = NotesOrganizer()
    
    while True:
        print("\nNotes Organizer")
        print("1. Add Note")
        print("2. View Notes")
        print("3. Sort Notes")
        print("4. Delete Note")
        print("5. Exit")
        choice = input("Choose an option: ")
        
        if choice == "1":
            title = input("Enter title: ")
            content = input("Enter content: ")
            topic = input("Enter topic: ")
            organizer.add_note(title, content, topic)
        elif choice == "2":
            organizer.view_notes()
        elif choice == "3":
            print("Sort by: alphabetical, topic, or date")
            criterion = input("Enter sort criterion: ").lower()
            organizer.sort_notes(criterion)
        elif choice == "4":
            title = input("Enter the title of the note to delete: ")
            organizer.delete_note(title)
        elif choice == "5":
            print("Exiting Notes Organizer. Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
