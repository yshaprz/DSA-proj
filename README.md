# DSA-proj
# Student Grade Calculator

# Calculate the Average of Grade using loops and conditional statements
def calcu_ave(grades):
    total = 0
    count = 0

    for grade in grades:
        total += grade
        count += 1

    return total / count if count > 0 else 0

# Merge sort function for sorting alphabetically
def merge_sort(arr, key):
    if len(arr) > 1:
        mid = len(arr) // 2
        left_half, right_half = arr[:mid], arr[mid:]

        merge_sort(left_half, key)
        merge_sort(right_half, key)

        arr[:] = merge(left_half, right_half, key)

def merge(left, right, key):
    result = []
    i = j = 0

    while i < len(left) and j < len(right):
        if key(left[i]) < key(right[j]):
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])
    return result

# Input validation function
def input_valid(prompt, minimum, maximum):
    while True:
        try:
            value = int(input(prompt))
            if minimum <= value <= maximum:
                return value
            else:
                print(f"\nENTER A VALUE BETWEEN {minimum} and {maximum} ONLY.")
        except ValueError:
            print("\nERROR! PLEASE TRY AGAIN.")

# Display results
def display_table(students):
    print("{:<4} {:<25} {:<15}".format("#", "Student Name", "Average Grade"))
    print("---------------------------------------------------")

    for i, (name, grades) in enumerate(students, 1):
        average_grade = calcu_ave(grades)
        print("{:<4} {:<25} {:<15.2f}".format(i, name, average_grade))

# Function to extract the name for sorting
def get_names(student):
    return student[0]

# Function to extract the average grade for sorting
def get_grades(student):
    return calcu_ave(student[1])

def main():
    number_subjects = input_valid("\nENTER THE NUMBER OF SUBJECTS (between 1 and 10 subjects only): ", 1, 10)
    number_students = input_valid("\nENTER THE NUMBER OF STUDENTS (between 1 and 25 students only): ", 1, 25)
    students_list = [
        (
            input(f"\nENTER THE STUDENT #{i + 1} NAME: "),
            [float(input(f"ENTER THE GRADE FOR SUBJECT #{j + 1}: ")) for j in range(number_subjects)],
        )
        for i in range(number_students)
    ]

    # Sorting names alphabetically using merge sort
    merge_sort(students_list, key=get_names)
    print("\nLIST OF STUDENT'S NAMES ALPHABETICALLY WITH THEIR CORRESPONDING AVERAGES: ")
    display_table(students_list)

    # Sorting grades in descending order
    student_grade_sorted = sorted(students_list, key=get_grades, reverse=True)
    print("\nLIST OF STUDENT'S GRADE ARRANGED FROM HIGHEST TO LOWEST: ")
    display_table(student_grade_sorted)

if __name__ == "__main__":
    main()
