#include <iostream>
#include <fstream>

using namespace std;

//необходимые структуры;
struct Birthday
{
	int date;
	int month;
	int year;
	bool isCorrect();
};

struct Enrollee //абитуриент;
{
	char surname[56];
	char name[32];
	char patronomyc[56];
	char sex[10];
	char nationality[56];
	char country[32];
	char region[32];
	char city[32];
	char street[32];
	int index;
	int home;
	int apartment;
	int rating;
	int passing_score;
	Birthday DATE;
};

//функции корректности даты;
bool Birthday::isCorrect()
{
	bool result = false;
	switch (month)
	{
	case 1:
	case 3:
	case 5:
	case 7:
	case 8:
	case 10:
	case 12:
	{
		if ((date <= 31) && (date > 0))
			result = true;
		break;
	}

	case 4:
	case 6:
	case 9:
	case 11:
	{
		if ((date <= 30) && (date > 0))
			result = true;
		break;
	}

	case 2:
	{
		if (year % 4 != 0)
		{
			if ((date <= 28) && (date > 0))
				result = true;
		}
		else
			if (year % 400 == 0)
			{
				if ((date <= 29) && (date > 0))
					result = true;
			}
			else
				if ((year % 100 == 0) && (year % 400 != 0))
				{
					if ((date == 28) && (date > 0))
						result = true;
				}
				else
					if ((year % 4 == 0) && (year % 100 != 0))
						if ((date <= 29) && (date > 0))
							result = true;
		break;
	}

	default:
		result = false;
	}

	return result;
}

void easy()
{
	cout << endl;
	cout << "Необходимо считать произвольную информацию из файла," << endl;
	cout << "переписать данную информацию в зависимости от задания," << endl;
	cout << "а также сохранить эту информацию в новый файл" << endl << endl;

	char symbol;

	string read = "Old_file.txt"; //файл к которому мы будем обращаться;
	string new_read = "New_file.txt";

	ofstream write; //создаем переменную создания/открытия файла;
	ofstream new_write;

	ifstream console; //создаем переменную вызова файла;

	console.open(read);

	if (!console.is_open()) //если не удается открыть файл - выдаем сообщение;
	{
		cout << "Не удалось открыть или найти необходимый файл!" << endl << endl;
	}

	else
	{
		cout << "Файл открыт! В данном файле записано: " << endl;

		while (console.get(symbol)) //посимвольно считываем в консоль данные из файла;
		{
			cout << symbol;
		}

		cout << endl;
		cout << "------------------------------------------------" << endl << endl;
	}

	console.close(); //закрываем файл;

	cout << "Необходимо вывести в файл информацию об абитуриентах, чей проходной балл выше 4" << endl << endl;

	Enrollee* arr;
	int size, count;

	do
	{
		cout << "Введите количество абитуриентов, данные которых вы будете вводить: ";
		cin >> size;
	} while (size < 1);

	arr = new Enrollee[size];

	cout << endl;

	//ввод необходимой информации со всеми проверками;
	for (int i = 0; i < size; i++)
	{
		cout << "Введите фамилию абитуриента под номером " << i + 1 << ": ";
		cin.ignore(cin.rdbuf()->in_avail());
		cin.getline(arr[i].surname, 56);
		cout << endl;

		cout << "Введите имя: ";
		cin.ignore(cin.rdbuf()->in_avail());
		cin.getline(arr[i].name, 56);
		cout << endl;

		cout << "Введите отчество: ";
		cin.ignore(cin.rdbuf()->in_avail());
		cin.getline(arr[i].patronomyc, 56);
		cout << endl;

		cout << "Введите пол: ";
		cin.ignore(cin.rdbuf()->in_avail());
		cin.getline(arr[i].sex, 10);
		cout << endl;

		cout << "Введите национальность: ";
		cin.ignore(cin.rdbuf()->in_avail());
		cin.getline(arr[i].nationality, 56);
		cout << endl;

		do
		{
			cout << "Введите День Рождения: ";
			cin >> arr[i].DATE.date;
			cout << endl;
			cout << "Месяц: ";
			cin >> arr[i].DATE.month;
			cout << endl;
			cout << "Год: ";
			cin >> arr[i].DATE.year;
			cout << endl;
		} while (!arr[i].DATE.isCorrect());

		do
		{
			count = 0;

			cout << "Введите почтовый индекс: ";
			cin.ignore(cin.rdbuf()->in_avail());
			cin >> arr[i].index;

			if (arr[i].index < 100000 && arr[i].index >= 10000)
			{
				count++;
			}
			cout << endl;

		} while (count == 0);

		cout << "Введите страну: ";
		cin.ignore(cin.rdbuf()->in_avail());
		cin.getline(arr[i].country, 32);
		cout << endl;

		cout << "Введите регион: ";
		cin.ignore(cin.rdbuf()->in_avail());
		cin.getline(arr[i].region, 32);
		cout << endl;

		cout << "Введите город: ";
		cin.ignore(cin.rdbuf()->in_avail());
		cin.getline(arr[i].city, 32);
		cout << endl;

		cout << "Введите улицу: ";
		cin.ignore(cin.rdbuf()->in_avail());
		cin.getline(arr[i].street, 32);
		cout << endl;

		cout << "Введите номер дома: ";
		cin >> arr[i].home;
		cout << endl;

		cout << "Введите номер квартиры: ";
		cin >> arr[i].apartment;
		cout << endl;

		cout << "Введите средний балл: ";
		cin >> arr[i].rating;
		cout << endl;

		cout << "Введите проходной балл: ";
		cin >> arr[i].passing_score;
		cout << endl;
	}

	//выводим в оба файла необходимую информацию;
	write.open(read);
	new_write.open(new_read); //открытие файла с именем "new_read";

	int count2 = 0;

	write << "Информация об абитуриентах с проходным баллом больше 4" << endl << endl;
	new_write << "Информация об абитуриентах с проходным баллом больше 4 " << endl << endl;

	for (int i = 0; i < size; i++)
	{
		if (arr[i].passing_score > 4)
		{
			if (!write.is_open()) //если не удается открыть файл - выдаем сообщение;
			{
				cout << "Не удалось открыть или найти необходимый файл!" << endl;
			}

			else
			{
				write << "Фамилия абитуриента под номером " << i + 1 << ": " << arr[i].surname << ", Имя: " << arr[i].name << ", Отчество: " << arr[i].patronomyc << endl;
				write << "Пол: " << arr[i].sex << ", Национальность: " << arr[i].nationality << ", Дата Рождения: " << arr[i].DATE.date << " " << arr[i].DATE.month << " " << arr[i].DATE.year << endl;
				write << "Почтовый индекс: " << arr[i].index << ", Страна: " << arr[i].country << ", Регион: " << arr[i].region << ", Город: " << arr[i].city << endl;
				write << "Улица: " << arr[i].street << ", Дом: " << arr[i].home << ", Квартира: " << arr[i].apartment << ", Средний балл: " << arr[i].rating << ", Проходной балл: " << arr[i].passing_score << endl << endl;
				count2++;
			}

			if (!new_write.is_open())
			{
				cout << "Не удалось открыть или найти необходимый файл!" << endl;
			}

			else
			{
				new_write << "Фамилия абитуриента под номером " << i + 1 << ": " << arr[i].surname << ", Имя: " << arr[i].name << ", Отчество: " << arr[i].patronomyc << endl;
				new_write << "Пол: " << arr[i].sex << ", Национальность: " << arr[i].nationality << ", Дата Рождения: " << arr[i].DATE.date << " " << arr[i].DATE.month << " " << arr[i].DATE.year << endl;
				new_write << "Почтовый индекс: " << arr[i].index << ", Страна: " << arr[i].country << ", Регион: " << arr[i].region << ", Город: " << arr[i].city << endl;
				new_write << "Улица: " << arr[i].street << ", Дом: " << arr[i].home << ", Квартира: " << arr[i].apartment << ", Средний балл: " << arr[i].rating << ", Проходной балл: " << arr[i].passing_score << endl << endl;
				count2++;
			}
		}
	}

	//если абитуриентов с заданным условием не найдено - записываем в файл сообщение;
	if (count2 == 0)
	{
		write << "Нет абитуриентов с проходным баллом больше 4";
		new_write << "Нет абитуриентов с проходным баллом больше 4";
	}

	cout << endl << "Соответсвенная информация вывелась в текстовый файл";
	cout << endl << endl;
}

void medium()
{
	cout << endl << "Необходимо считать из файла символы и записать их в другой файл при помощи третьего файла" << endl << endl;

	char arr[50], arr1[50], symbol, symbol1; //массивы и переменные для записи и считывания;
	int count = 0;

	string read = "F1.txt"; //файл к которому мы будем обращаться;
	string new_read = "F2.txt";
	string help = "H.txt";

	ofstream write; //создаем файловую переменную;

	ifstream console;

	console.open(read);

	if (!console.is_open()) //если не удается открыть файл - выдаем сообщение;
	{
		cout << "Не удалось найти или открыть файл для считывания F1!" << endl;
	}

	else
	{
		cout << "Файл F1 открыт! В данном файле записано: " << endl;

		while (console.get(symbol)) //посимвольно считываем в консоль данные из файла;
		{
			count++;
			for (int i = count; i <= count; i++)
			{
				arr[i] = symbol;
				cout << arr[i];
			}
		}
	}

	console.close(); //закрываем файл;

	cout << endl << endl;

	write.open(help); //открываем вспомогательный файл для записи информации в него;

	if (!write.is_open())
	{
		cout << "Не удалось открыть или найти вспомогательный файл H для записи!" << endl;
	}

	else
	{
		cout << "Информация была записана в вспомогательный файл H" << endl;
		for (int i = 1; i <= count; i++)
		{
			write << arr[i];
		}
	}

	cout << endl << endl;

	write.close();

	console.open(help); //считываем данные в консоль из вспомогательного файла;

	count = 0;

	if (!console.is_open())
	{
		cout << "Не удалось найти или открыть вспомогательный файл H для считывания!" << endl;
	}

	else
	{
		cout << "Файл H открыт! В вспомогательном файле записано: " << endl;

		while (console.get(symbol1)) //посимвольно считываем в консоль данные из файла;
		{
			count++;
			for (int i = count; i <= count; i++)
			{
				arr1[i] = symbol1;
				cout << arr1[i];
			}
		}
	}

	console.close();

	cout << endl << endl;

	write.open(new_read); //записываем данные в финальный файл F2, после чего закрываем его;

	if (!write.is_open()) //если не удается открыть файл - выдаем сообщение;
	{
		cout << "Не удалось открыть или найти файл F2!" << endl;
	}

	else
	{
		cout << "Информация была записана в файл F2" << endl;
		for (int i = 1; i <= count; i++)
		{
			write << arr1[i];
		}
	}

	write.close();

	cout << endl << endl;
}

void hard()
{
        cout << "Необходимо создать k квадратных матриц, записать их в первый файл" << endl;
        cout << "Из данных матриц транспонированные записать во второй файл, не трансп. - в третий файл" << endl;
        cout << "Вывести на экран данные из файлов" << endl << endl;

	int** arr, quantity, count = 0, count1 = 0, count2 = 0, count3 = 0, count4 = 0;
	char symbol;

	//Вводим кол-во матриц;
	cout << endl << "Введите количество матриц для записи в 1-й файл: ";

	cin >> quantity;

	cout << endl;

	//создаем двумерный динамический массив;
	arr = new int* [3];

	for (int i = 0; i < 3; i++)
	{
		arr[i] = new int[3];
	}

	string read = "One_hard.txt"; //файлы с которыми мы будем работать;
	string read_1 = "Two_hard.txt";
	string read_2 = "Three_hard.txt";

	ofstream write, write1, write2;

	//открываем все 3 файла;
	write.open(read);
	write1.open(read_1);
	write2.open(read_2);

	if (!write.is_open()) //если не удается открыть файл - выдаем сообщение;
	{
		cout << endl << "Не удалось открыть или найти необходимый первый файл!" << endl;
	}

	//записываем в первый файл введенное кол-во матриц;
	else
	{
		cout << endl << "В файл № 1 записано заданное кол-во матриц, в №2 и №3 - трансп. и не трансп. матрицы среди данных" << endl << endl;
		write << "Массивы первого файла: " << endl << endl;

		for (int k = 0; k < quantity; k++)
		{
			for (int i = 0; i < 3; i++)
			{
				for (int j = 0; j < 3; j++)
				{
					arr[i][j] = rand() % -2 + 2;
					write << arr[i][j] << "\t";
					count++;
				}

				//если элемент матрицы последний - проверяем на транспонированность;
				if (count % 9 == 0)
				{
					if(arr[0][0] == arr[0][2] && arr[0][2] == arr[2][2] && arr[2][2] == arr[2][0])
					{
						if (arr[0][1] == arr[1][2] && arr[1][2] == arr[2][1] && arr[2][1] == arr[1][0])
						{
							if (!write1.is_open()) //если не удается открыть файл - выдаем сообщение;
							{
								count2++;
								if(count2 == 1)
								{
									cout << endl << "Не удалось открыть или найти необходимый второй файл!" << endl;
									cout << "Транспонированные матрицы не будут записаны в него" << endl;
								}
							}

							//записываем трансп. матрицу во второй файл;
							else 
							{
								for (int i = 0; i < 3; i++)
								{
									for (int j = 0; j < 3; j++)
									{
										write1 << arr[i][j] << "\t";
									}

									write1 << endl;
								}

								write1 << endl;

								count1++;
							}
						}
					}

					//если матрица не транспонированная - записываем ее в третий файл;
					else
					{
						if (!write2.is_open()) //если не удается открыть файл - выдаем сообщение;
						{
							count3++;
							if (count3 == 1)
							{
								cout << endl << "Не удалось открыть или найти необходимый третий файл!" << endl;
								cout << "Не трансп. матрицы не будут записаны в него" << endl;
							}
						}

						else
						{
							for (int i = 0; i < 3; i++)
							{
								for (int j = 0; j < 3; j++)
								{
									write2 << arr[i][j] << "\t";
								}

								write2 << endl;
							}

							write2 << endl;

							count4++;
						}
					}
				}

				write << endl;
			}

			write << endl;
		}
	}

	//если не встретилась не одна матрица какого-либо типа - выдаем сообщение;
	if (count1 == 0)
	{
		write1 << "Нет транспонированных среди матриц первого файла";
	}

	if (count4 == 0)
	{
		write2 << "Нет не трасп. матриц среди матриц первого файла";
	}

	write.close();
	write1.close();
	write2.close();

	ifstream console, console1, console2;

	//выводим содержимое файлов на экран;
	console.open(read);
	console1.open(read_1);
	console2.open(read_2);

	if (!console.is_open()) //если не удается открыть файл - выдаем сообщение;
	{
		cout << endl << "Не удалось открыть или найти первый файл!" << endl;
	}

	else
	{
		cout << endl << "Файл номер 1 открыт! В данном файле записано: " << endl << endl;

		while (console.get(symbol)) //посимвольно считываем в консоль данные из файла;
		{
			cout << symbol;
		}
	}

	if (!console1.is_open()) //если не удается открыть файл - выдаем сообщение;
	{
		cout << endl << "Не удалось открыть или найти второй файл!" << endl;
	}

	else
	{
		cout << endl << "Файл номер 2 открыт! В данном файле записано: " << endl << endl;

		while (console1.get(symbol)) //посимвольно считываем в консоль данные из файла;
		{
			cout << symbol;
		}

		cout << endl;
	}

	if (!console2.is_open()) //если не удается открыть файл - выдаем сообщение;
	{
		cout << endl << "Не удалось открыть или найти третий файл!" << endl;
	}

	else
	{
		cout << endl << "Файл номер 3 открыт! В данном файле записано: " << endl << endl;

		while (console2.get(symbol)) //посимвольно считываем в консоль данные из файла;
		{
			cout << symbol;
		}

		cout << endl;
	}

	cout << endl << endl;
}

int main()
{
	setlocale(LC_ALL, "ru");

	int a;
	int count = 0;

	do
	{
		cout << "Введите номер задания (easy - 1), (medium - 2), (hard - 3): ";

		cin >> a;

		cout << endl;

		if (a == 1)
		{
			easy();
			count++;
		}

		if (a == 2)
		{
			medium();
			count++;
		}

		if (a == 3)
		{
			hard();
			count++;
		}

	} while (count == 0);

	int b;

	do
	{
		count = 0;

		cout << "Продолжить ввод? Да - 1, Нет - 2: ";

		cin >> b;

		cout << endl;

		if (b == 1)
		{
			count++;
			main();
		}

		if (b == 2)
		{
			cout << "Вы решили не продолжать";
			count++;
			break;
		}

	} while (count == 0);
}
