# Parallelogramm
#include <iostream>
#include <iomanip>
#include <cmath>
#include <ctime>
#include <string>
#include <cstdlib>

using namespace std;

class Paralelogram {
public:
	int SetAngle(int Angle);    // Установка угла
	void ShowAngle();           // Вывести на экран угол

	double SetSide(int NumerSide, double Num, char Simv = '.');  // Установить значения  угла
																 // Небольшое пояснение к функции 
																 // (Номер угла, Число на которое нужно изменить, Символ обозначающий прибавление или отрицание угла (не обязательный))

																 // Если не указать 3-й параметр, то будет просто установленно значение в нужную сторону без учета %

	void ShowSide(int NumeSide);    // Показать значение из сторон
	double CalculationArea();       // Вычисление площади 
	double CalculationDiagonal();   // Вычисление диагонали
	double CalculationHeight();     // Вычисление высоты





	Paralelogram() {} // Конструктор
	~Paralelogram() {}// Деструктор
private:
	double Area;            // Площадь
	double Height = 0;      // Значение высоты
	int Angle = 0;          // Угол между сторонами
	double Side1;       // 1-я сторона - ОСНОВАНИЕ !!!!
	double Side2;       // 2-я сторона
};

int Paralelogram::SetAngle(int Angle) {
	this->Angle = Angle;
	return this->Angle;
}

void Paralelogram::ShowAngle() {
	cout << "\n Угол = " << this->Angle;
}

double Paralelogram::SetSide(int NumerSide, double Num, char Simv)
{
	double Perc = 0.0;
	if ((Simv == '+' || '-') && NumerSide == 1) Perc = (Side1 * (Num / 100));


	if ((Simv == '+' || '-') && NumerSide == 2) Perc = (Side2 * (Num / 100));

	switch (Simv)
	{

	case '+':   // Увеличиваем значение на Num %
	{
		if (NumerSide == 1)
		{
			Side1 += Perc;
			return Side1;
		}
		else if (NumerSide == 2)
		{
			Side2 += Perc;
			return Side2;
		}
		break;
	}

	case '-':   // Уменьшаем значение на Num %
	{
		if (NumerSide == 1)
		{
			Side1 -= Perc;
			return Side1;
		}
		else if (NumerSide == 2)
		{
			Side2 -= Perc;
			return Side2;
		}
		break;
	}

	default:    // Если параметр не задан, то простая установка
	{
		if (NumerSide == 1)
		{
			Side1 = Num;
			return Side1;
		}

		else if (NumerSide == 2)
		{
			Side2 = Num;
			return Side2;
		}
		break;
	}

	}

}

void Paralelogram::ShowSide(int NumerSide) {
	if (NumerSide == 1) cout << "Основание = " << Side1;
	if (NumerSide == 2) cout << "2-я сторона = " << Side2;
}

double Paralelogram::CalculationArea() {
	int state = 0;
	if ((Height != 0) && (Angle != 0))  // Узнаем, если имеется и высота и угол, то делаем выбор
	{
		cout
			<< "\n Так как имеется данные о высоте и угле,"
			<< "\n можно выбрать способ расчета:"
			<< "\n 1. Использовать угол"
			<< "\n 2. Использовать высоту";

		cin >> state;
	}
	if ((Height = 0) && (Angle != 0))   // если есть только угол
		state = 1;
	if ((Height != 0) && (Angle = 0))   // если есть только высота
		state = 2;

	if ((Height = 0) && (Angle = 0)) {  // если нет ничего
		cout << "\n\n Нет необходимых данных для расчета";
		return -1;                      // Значение если ошибка
	}

	switch (state)
	{
	case 1:
	{
		Area = (Side1 * Side2) * (sin(Angle));
		return Area;
	}

	case 2:
	{
		Area = Side1 * Height;
		return Area;
	}
	}


}

double Paralelogram::CalculationDiagonal() {
	if (Angle != 0) {
		cout << "\n Вычисление диагонали по теореме косинусов: "
			<< "D = в€љa^2 + b^2 - 2ab * cosО±"
			<< "\n D = " << "в€љ" << Side1 << "^2 + " << Side2 << "^2 - 2" << Side1 << Side2 << "cos" << Angle;
		double D;
		D = sqrt(((Side1 * Side1) + (Side2 * Side2)) - (2 * (Side1 * Side2)) * cos(Angle));

		return D;
	}
	else cout << "\n\n Нет необходимых данных. Проверьте значения";
}

double Paralelogram::CalculationHeight() {
	if ((Area != 0) && (Angle != 0)) {
		Height = (Area / Angle);
		return Height;
	}
	else cout << "\n\n Отсутствуют необходимые значения";
}

int main()
{

	setlocale(0, "");               // Установка русского языка

	Paralelogram Par;               // Создание переменной параллелограмма

	cout << "Введите угол: ";
	int Angle;
	cin >> Angle;
	cout << "\n\n Угол параллелограмма = " << Par.SetAngle(Angle);
	double Side;
	cout << "\n\n Введите значение 1 стороны: ";
	cin >> Side;
	Side = Par.SetSide(1, Side); // 1 угол = 50 гр.
	cout << "\n\n Введите значение 2 стороны: ";
	Side = Par.SetSide(2, Side); // 2 угол = 30 гр.

	double Area = Par.CalculationArea();
	cout << "Площадь = " << Area;

	system("pause");
	return 0;
}
