# number-analysis2
# Algoritms: Atzīmju analīze

# Importējam nepieciešamās bibliotēkas
import csv

# Funkcija, lai aprēķinātu statistiku
def calculate_statistics(grades):
    """
    Aprēķina vidējo, augstāko un zemāko atzīmi.
    """
    # Pārbaudām, vai saraksts nav tukšs
    if len(grades) == 0:
        return 0, 0, 0  # Ja tukšs, atgriežam 0 vērtības

    # Aprēķinām vidējo atzīmi
    total = sum(grades)  # Kopējā atzīme
    count = len(grades)  # Atzīmju skaits
    average = total / count  # Vidējā atzīme

    # Atrodam augstāko un zemāko atzīmi
    highest = max(grades)
    lowest = min(grades)

    return average, highest, lowest  # Atgriežam rezultātus

# Funkcija, lai grupētu studentus
def group_students(students, grades, average):
    """
    Grupē studentus, balstoties uz vidējo atzīmi.
    """
    above_average = []  # Saraksts studentiem virs vidējās atzīmes
    below_average = []  # Saraksts studentiem zem vidējās atzīmes

    # Grupējam studentus
    for i in range(len(grades)):
        if grades[i] > average:
            above_average.append(students[i])
        else:
            below_average.append(students[i])

    return above_average, below_average  # Atgriežam grupas

# Funkcija, lai saglabātu datus CSV failā
def save_to_csv(students, grades, filename="results.csv"):
    """
    Saglabā studentu vārdus un atzīmes CSV failā.
    """
    with open(filename, mode="w", newline="") as file:
        writer = csv.writer(file)
        writer.writerow(["Students", "Atzīme"])  # Raksta virsrakstus

        # Raksta katru studentu un atzīmi
        for i in range(len(students)):
            writer.writerow([students[i], grades[i]])

# Funkcija, lai izvadītu statistiku
def print_statistics(average, highest, lowest):
    """
    Izvada statistiku par atzīmēm.
    """
    print(f"Vidējā atzīme: {average:.2f}")  # Izvada vidējo atzīmi
    print(f"Augstākā atzīme: {highest}")  # Izvada augstāko atzīmi
    print(f"Zemākā atzīme: {lowest}")  # Izvada zemāko atzīmi

# Funkcija, lai izvadītu studentu grupas
def print_student_groups(above_average, below_average):
    """
    Izvada studentu grupas.
    """
    print("Studenti virs vidējās atzīmes:", above_average)  # Virs vidējās
    print("Studenti zem vidējās atzīmes:", below_average)  # Zem vidējās

# Galvenā programma
if __name__ == "__main__":
    # Ievaddati
    students = ["Anna", "Jānis", "Līga", "Pēteris", "Zane"]  # Studentu vārdi
    grades = [8, 6, 9, 5, 7]  # Studentu atzīmes

    # Aprēķina statistiku
    average, highest, lowest = calculate_statistics(grades)

    # Izvada statistiku
    print_statistics(average, highest, lowest)

    # Grupē studentus
    above_average, below_average = group_students(students, grades, average)

    # Izvada studentu grupas
    print_student_groups(above_average, below_average)

    # Saglabā rezultātus CSV failā
    save_to_csv(students, grades)
    print("Rezultāti saglabāti 'results.csv' failā.")  # Paziņojums par saglabāšanu

# Beigas
print("Programma pabeigta.")  # Paziņojums par programmas beigām
