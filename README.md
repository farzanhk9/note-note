import json
from datetime import datetime

FILENAME = "notes.json"

def load_notes():
    try:
        with open(FILENAME, "r") as f:
            return json.load(f)
    except FileNotFoundError:
        return []

def save_notes(notes):
    with open(FILENAME, "w") as f:
        json.dump(notes, f, indent=4)

def add_note():
    note = input("Write your note: ")
    notes = load_notes()
    notes.append({"note": note, "time": datetime.now().strftime("%Y-%m-%d %H:%M")})
    save_notes(notes)
    print("✅ Note saved!")

def show_notes():
    notes = load_notes()
    if not notes:
        print("📭 No notes found.")
    else:
        print("\n=== YOUR NOTES ===")
        for i, n in enumerate(notes, 1):
            print(f"{i}. {n['note']} ({n['time']})")

def main():
    while True:
        print("\nOptions:")
        print("1. Add note")
        print("2. Show notes")
        print("3. Exit")
        choice = input("Choose: ")

        if choice == "1":
            add_note()
        elif choice == "2":
            show_notes()
        elif choice == "3":
            break
        else:
            print("⚠️ Invalid choice!")

if __name__ == "__main__":
    main()
