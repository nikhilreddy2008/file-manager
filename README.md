# file-manager
python project
import os
import shutil

def show_menu():
    print("\n===== Simple File Manager =====")
    print("1. List files")
    print("2. Create new folder")
    print("3. Delete a file/folder")
    print("4. Rename a file/folder")
    print("5. Move a file")
    print("6. Copy a file")
    print("7. Exit")
    print("===============================")

def list_files(path):
    print(f"\nFiles in {path}:")
    for item in os.listdir(path):
        print(" -", item)

def create_folder(path):
    name = input("Enter folder name: ")
    new_path = os.path.join(path, name)
    os.makedirs(new_path, exist_ok=True)
    print(f"✅ Folder '{name}' created!")

def delete_item(path):
    name = input("Enter file/folder name to delete: ")
    target = os.path.join(path, name)
    if os.path.isfile(target):
        os.remove(target)
        print("🗑 File deleted.")
    elif os.path.isdir(target):
        shutil.rmtree(target)
        print("🗑 Folder deleted.")
    else:
        print("❌ Item not found.")

def rename_item(path):
    name = input("Enter file/folder name to rename: ")
    new_name = input("Enter new name: ")
    os.rename(os.path.join(path, name), os.path.join(path, new_name))
    print("✅ Renamed successfully.")

def move_file(path):
    name = input("Enter file name to move: ")
    dest = input("Enter destination folder path: ")
    shutil.move(os.path.join(path, name), dest)
    print("✅ File moved successfully.")

def copy_file(path):
    name = input("Enter file name to copy: ")
    dest = input("Enter destination folder path: ")
    shutil.copy(os.path.join(path, name), dest)
    print("✅ File copied successfully.")

def main():
    path = os.getcwd()
    while True:
        show_menu()
        choice = input("Enter choice (1-7): ")

        if choice == "1":
            list_files(path)
        elif choice == "2":
            create_folder(path)
        elif choice == "3":
            delete_item(path)
        elif choice == "4":
            rename_item(path)
        elif choice == "5":
            move_file(path)
        elif choice == "6":
            copy_file(path)
        elif choice == "7":
            print("👋 Exiting File Manager. Bye!")
            break
        else:
            print("❌ Invalid choice. Try again.")

if __name__ == "__main__":
    main()
