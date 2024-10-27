using System;
using System.Collections.Generic;

namespace MedicalRecords
{
    class Program
    {
        static void Main(string[] args)
        {
            List<MedicalRecord> records = new List<MedicalRecord>();
            int choice;

            do
            {
                Console.WriteLine("1. Добавить запись");
                Console.WriteLine("2. Просмотреть записи");
                Console.WriteLine("3. Удалить запись");
                Console.WriteLine("0. Выход");
                Console.Write("Выберите опцию: ");
                choice = Convert.ToInt32(Console.ReadLine());

                switch (choice)
                {
                    case 1:
                        AddRecord(records);
                        break;
                    case 2:
                        ViewRecords(records);
                        break;
                    case 3:
                        DeleteRecord(records);
                        break;
                    case 0:
                        Console.WriteLine("Выход из программы.");
                        break;
                    default:
                        Console.WriteLine("Неверный выбор. Попробуйте снова.");
                        break;
                }

            } while (choice != 0);
        }

        static void AddRecord(List<MedicalRecord> records)
        {
            Console.Write("Введите имя пациента: ");
            string patientName = Console.ReadLine();
            Console.Write("Введите диагноз: ");
            string diagnosis = Console.ReadLine();
            Console.Write("Введите дату записи (YYYY-MM-DD): ");
            DateTime date = DateTime.Parse(Console.ReadLine());

            records.Add(new MedicalRecord { PatientName = patientName, Diagnosis = diagnosis, Date = date });
            Console.WriteLine("Запись добавлена!");
        }

        static void ViewRecords(List<MedicalRecord> records)
        {
            Console.WriteLine("\n--- Медицинские записи ---");
            foreach (var record in records)
            {
                Console.WriteLine(record);
            }
            Console.WriteLine("--------------------------\n");
        }

        static void DeleteRecord(List<MedicalRecord> records)
        {
            Console.Write("Введите индекс записи для удаления (начинается с 0): ");
            int index = Convert.ToInt32(Console.ReadLine());

            if (index >= 0 && index < records.Count)
            {
                records.RemoveAt(index);
                Console.WriteLine("Запись удалена!");
            }
            else
            {
                Console.WriteLine("Неверный индекс.");
            }
        }
    }

    class MedicalRecord
    {
        public string PatientName { get; set; }
        public string Diagnosis { get; set; }
        public DateTime Date { get; set; }

        public override string ToString()
        {
            return $"Пациент: {PatientName}, Диагноз: {Diagnosis}, Дата: {Date.ToShortDateString()}";
        }
    }
}
