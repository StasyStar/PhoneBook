# Программа Телефонный справочник, которая имеет следующие функции:
1. Программа должна выводить данные
2. Программа должна сохранять данные в текстовом файле
3. Пользователь может ввести одну из характеристик для поиска определенной записи(Например имя или фамилию человека)
4. Использование функций. Ваша программа не должна быть линейной
5. Экспорт и импорт данных из одного файла в другой
6. Редактирование и удаление данных

## 1. Создание файла
## 2. Добавление новой записи
- запросить ввод у пользователя
- открытие файла на дополнительные записи
- добавить запись в файл
```
def surname_input():
    return input('Введите фамилию: ').title()

def name_input():
    return input('Введите имя: ').title()

def patronymic_input():
    return input('Введите отчество: ').title()

def phone_input():
    return input('Введите номер: ')

def address_input():
    return input('Введите адрес: ').title()

def create_contacts():
    surname = surname_input()
    name = name_input()
    patronymic = patronymic_input()
    phone = phone_input()
    address = address_input()
        
    return f'{surname} {name} {patronymic} {phone}\n{address}\n\n'

def write_contact():
    contact = create_contacts()
    with open('phonebook.txt', 'a', encoding='UTF-8') as file: 
        file.write(contact)
        print('\nКонтакт записан.\n')
```
## 3. Вывод на экран
- открытие файла для чтения
- считывание данных
- вывод на экран
```
def read_files():
    with open('phonebook.txt', 'r', encoding='UTF-8') as file: 
        contact_list = file.read().rstrip().split('\n\n')
    return contact_list

def print_contacts():
    contact_list = read_files()
    for nn, contact in enumerate(contact_list, 1):
        print(f'{nn}. {contact}\n')
```
## 4. Поиск контакта
- выбрать вариант поиска (фамилия, телефон и т.д.)
- запросить ввод у пользователя
- открытие файла для чтения
- считать данные
- осуществить поиск
- вывести результат поиска
```
def search_contacts():
    print(
        'Возможные варианты поиска:\n'
        '1. По фамилии\n'
        '2. По имени\n'
        '3. По отчеству\n'
        '4. По телефону\n'
        '5. По адресу\n'
        )

    index_var = int(input('Выберите вариант поиска:\n')) - 1
        
    search = input('Введите данные для поиска: ').capitalize()
    with open('phonebook.txt', 'r', encoding='UTF-8') as file:
        contact_str = file.read()
        
    contact_list = contact_str.rstrip().split('\n\n')
    
    for contact_str in contact_list:
        contact_list = contact_str.replace('\n', ' ').split(' ')
        if search in contact_list[index_var]:
            print(f'\n{contact_str}\n')
```
## 5. Экспорт данных
- выбрать номера строк для экпорта
- запросить ввод у пользователя
- записать данные в новый файл
```
def export_contact():
    contact_list = read_files()
    print_contacts()
    num_contact = int(input('Введите номер контакта для экспорта: '))
    with open('export_phonebook.txt', 'a', encoding='utf-8') as file:
        file.write(contact_list[num_contact - 1])
        print('\nКонтакт экспортирован.\n')
```
## 6. Импорт данных
- открыть нужный файл
- скопировать нужные данные в текущий файл
```
def import_contact():
    with open('import_phonebook.txt', 'r', encoding='UTF-8') as file: 
        contact_list = file.read().rstrip().split('\n\n')
        for nn, contact in enumerate(contact_list, 1):
            print(f'{nn}. {contact}\n')
    num_contact = int(input('Введите номер контакта для импорта: '))
            
    with open('phonebook.txt', 'a', encoding='utf-8') as file:
        file.write(f'\n{contact_list[num_contact - 1]}\n')
        print('\nКонтакт импортирован.\n')
```
## 7. Редактирование данных
- выбрать номера строк для редактирования
- выбрать данные для редактирвоания
- запросить ввод у пользователя
- перезаписать данные
```
def edit_contact():
    contact_list = read_files()
    print_contacts()
    wrong_data = input('Введите данные, которые подлежат изменению: \n').capitalize()
    correct_data = input('Введите корректные данные: \n').capitalize()
    new_list = []
    for data in contact_list:      
        new_list.append(data.replace(wrong_data, correct_data))
    with open('phonebook.txt', 'w', encoding='utf-8') as file:
        for data in new_list:
            file.write(f'\n{data}\n')
            print('\nКонтакт изменен.\n')  
```
## 8. Удаление данных
- выбрать номера строк для удаления
- запросить ввод у пользователя
- удалить выбранные строки
```
def del_contact():
    contact_list = read_files()
    print_contacts()
    num_contact = int(input('Введите номер контакта, который нужно удалить: ')) - 1
    with open('phonebook.txt', 'w', encoding='utf-8') as file:
        for i in range(len(contact_list)):
            if i != num_contact:  
                file.write((f'\n{contact_list[i]}\n')) 
        print('\nКонтакт удален.\n')
```
# 9. Создание интерфейса
```
def interface():
    with open('phonebook.txt', 'a'):
        pass
    
    user_input = None
    while user_input != '8':
        print('Возможные варианты действия:\n'
            '1. Добавить контакт\n'
            '2. Вывод списка контактов\n'
            '3. Поиск контакта\n'
            '4. Экспорт контакта\n'
            '5. Импорт контакта\n'
            '6. Редактирование контакта\n'
            '7. Удаление контакта\n'
            '8. Закрыть справочник\n'
        )

        user_input = input('Выберите вариант действия:\n')
        
        while user_input not in ('1', '2', '3', '4', '5', '6', '7', '8'):
            print('Некорректный ввод!')
            user_input = input('Выберите вариант действия: ')
            
        match(user_input):
            case '1':
                write_contact()
            case '2':
                print_contacts()
            case '3':
                search_contacts()   
            case '4':
                export_contact()   
            case '5':
                import_contact()   
            case '6':
                edit_contact()   
            case '7':
                del_contact() 
```
## Запуск программы
```
if __name__ == '__main__':
    interface()
```  