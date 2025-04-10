FILE_NAME = "music_collection.txt"

def add_album():
    album = input("Введите название альбома: ").strip()
    artist = input("Введите имя исполнителя: ").strip()
    year = input("Введите год выпуска: ").strip()
    
    with open(FILE_NAME, "a", encoding="utf-8") as file:
        file.write(f"{album}|{artist}|{year}\n")
    print("Альбом добавлен.")

def view_collection():
    try:
        with open(FILE_NAME, "r", encoding="utf-8") as file:
            for line in file:
                album, artist, year = line.strip().split("|")
                print(f"Альбом: {album}, Исполнитель: {artist}, Год: {year}")
    except:
        print("Коллекция пуста.")

def search_by_artist():
    name = input("Введите имя исполнителя: ").strip().lower()
    found = False
    try:
        with open(FILE_NAME, "r", encoding="utf-8") as file:
            for line in file:
                album, artist, year = line.strip().split("|")
                if artist.lower() == name:
                    print(f"Альбом: {album}, Год: {year}")
                    found = True
    except:
        pass
    if not found:
        print("Ничего не найдено.")

def delete_album():
    name = input("Введите название альбома для удаления: ").strip().lower()
    deleted = False
    try:
        with open(FILE_NAME, "r", encoding="utf-8") as file:
            lines = file.readlines()
        with open(FILE_NAME, "w", encoding="utf-8") as file:
            for line in lines:
                album, artist, year = line.strip().split("|")
                if album.lower() != name:
                    file.write(line)
                else:
                    deleted = True
    except:
        pass

    if deleted:
        print("Альбом удалён.")
    else:
        print("Альбом с таким названием не найден.")

def main():
    while True:
        print("\nМеню:")
        print("1. Добавить новый альбом")
        print("2. Переглянути всю коллекцию")
        print("3. Пошук альбомів за виконавцем")
        print("4. Видалити альбом")
        print("5. Вихід")
        
        choice = input("Оберіть дію (1-5): ").strip()
        
        if choice == "1":
            add_album()
        elif choice == "2":
            view_collection()
        elif choice == "3":
            search_by_artist()
        elif choice == "4":
            delete_album()
        elif choice == "5":
            print("Завершення програми.")
            break
        else:
            print("Невірний вибір. Спробуйте ще раз.")

if __name__ == "__main__":
    main()
