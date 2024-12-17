class Doctor:
    def __init__(self, doctor_id=0, name="", specialization="", working_time="", qualification="", room_number=0):
        self.doctor_id = doctor_id
        self.name = name
        self.specialization = specialization
        self.working_time = working_time
        self.qualification = qualification
        self.room_number = room_number

    def __str__(self):
        # Proper formatting for display alignment
        return f"{self.doctor_id:<5} {self.name:<20} {self.specialization:<16} {self.working_time:<16} {self.qualification:<16} {self.room_number:<7}"


class DoctorManager:
    def __init__(self):
        self.doctors_list = []
        self.read_doctors_file()

    def read_doctors_file(self):
        try:
            with open("doctors.txt", "r") as file:
                for line in file:
                    parts = line.strip().split("_")
                    if len(parts) == 6:
                        doctor = Doctor(int(parts[0]), parts[1], parts[2], parts[3], parts[4], int(parts[5]))
                        self.doctors_list.append(doctor)
        except FileNotFoundError:
            print("The file doctors.txt was not found.")

    def display_doctors_list(self):
        print("\nId    Name                 Speciality       Timing          Qualification    Room Number")

        for doctor in self.doctors_list:
            print(doctor)
            print() 

    def search_doctor_by_id(self):
        doctor_id = int(input("\nEnter the doctor Id: "))
        for doctor in self.doctors_list:
            if doctor.doctor_id == doctor_id:
                print("\nId    Name                 Speciality       Timing          Qualification    Room Number")
                print(doctor)
                print()
                return
        print("Can't find the doctor with the same ID on the system\n")

    def search_doctor_by_name(self):
        doctor_name = input("\nEnter the doctor name: ").strip()
        for doctor in self.doctors_list:
            if doctor.name == doctor_name:
                print("\nId    Name                 Speciality       Timing          Qualification    Room Number")
                print(doctor)
                print()
                return
        print("Can't find the doctor with the same name on the system\n")

    def add_dr_to_file(self):
        doctor_id = int(input("Enter the doctor’s ID: "))
        name = input("Enter the doctor’s name: ")
        specialization = input("Enter the doctor’s specialty: ")
        timing = input("Enter the doctor’s timing (e.g., 7am-10pm): ")
        qualification = input("Enter the doctor’s qualification: ")
        room_number = int(input("Enter the doctor’s room number: "))

        new_doctor = Doctor(doctor_id, name, specialization, timing, qualification, room_number)
        self.doctors_list.append(new_doctor)
        self.write_list_of_doctors_to_file()
        print(f"\nDoctor whose ID is {doctor_id} has been added\n")

    def edit_doctor_info(self):
        doctor_id = int(input("Please enter the ID of the doctor you want to edit: "))
        for doctor in self.doctors_list:
            if doctor.doctor_id == doctor_id:
                doctor.name = input("Enter new Name: ")
                doctor.specialization = input("Enter new Specialization: ")
                doctor.working_time = input("Enter new Timing: ")
                doctor.qualification = input("Enter new Qualification: ")
                doctor.room_number = int(input("Enter new Room Number: "))
                self.write_list_of_doctors_to_file()
                print(f"\nDoctor whose ID is {doctor_id} has been edited\n")
                return
        print("Cannot find the doctor with the entered ID\n")

    def write_list_of_doctors_to_file(self):
        with open("doctors.txt", "w") as file:
            for doctor in self.doctors_list:
                file.write(f"{doctor.doctor_id}_{doctor.name}_{doctor.specialization}_{doctor.working_time}_{doctor.qualification}_{doctor.room_number}\n")


class Patient:
    def __init__(self, patient_id=0, patient_name="", patient_disease="", patient_gender="", patient_age=0):
        self.patient_id = patient_id
        self.patient_name = patient_name
        self.patient_disease = patient_disease
        self.patient_gender = patient_gender
        self.patient_age = patient_age

    def __str__(self):
        return f"{self.patient_id:<4} {self.patient_name:<22} {self.patient_disease:<15} {self.patient_gender:<16} {self.patient_age:<16}"

class PatientManager:
    def __init__(self):
        self.patients_list = []
        self.read_patients_file()

    def read_patients_file(self):
        try:
            with open("patients.txt", "r") as file:
                for line in file:
                    parts = line.strip().split("_")
                    if len(parts) == 5:
                        patient = Patient(int(parts[0]), parts[1], parts[2], parts[3], int(parts[4]))
                        self.patients_list.append(patient)
        except FileNotFoundError:
            print("File 'patients.txt' not found. Starting with an empty list.")

    def display_patients_list(self):
        print("\nID   Name                   Disease         Gender          Age")
        for patient in self.patients_list:
            print(patient)
            print()

    def search_patient_by_id(self):
        patient_id = int(input("Enter the Patient Id: "))
        for patient in self.patients_list:
            if patient.patient_id == patient_id:
                print("\n\nID   Name                   Disease         Gender          Age")
                print(patient)
                print()
                return
        print("Can't find the Patient with the same ID on the system\n")

    def add_patient_to_file(self):
        patient_id = int(input("Enter Patients ID: "))
        patient_name = input("Enter Patient name: ")
        patient_disease = input("Enter Patient disease: ")
        patient_gender = input("Enter Patient gender: ")
        patient_age = int(input("Enter Patient age: "))

        new_patient = Patient(patient_id, patient_name, patient_disease, patient_gender, patient_age)
        self.patients_list.append(new_patient)
        self.write_list_of_patients_to_file()
        print(f"\nDoctor whose ID is {patient_id} has been added\n")

    def edit_patient_info(self):
        patient_id = int(input("Please enter the ID of the patient you want to edit: "))
        for patient in self.patients_list:
            if patient.patient_id == patient_id:
                patient.patient_name = input("Enter new Name: ")
                patient.patient_disease = input("Enter new disease: ")
                patient.patient_gender = input("Enter new gender: ")
                patient.patient_age = int(input("Enter new age: "))
                self.write_list_of_patients_to_file()
                print(f"\nDoctor whose ID is {patient_id} has been edited\n")
                return
        print("Cannot find the doctor with the entered ID\n")

    def write_list_of_patients_to_file(self):
        with open("patients.txt", "w") as file:
            for patient in self.patients_list:
                file.write(f"{patient.patient_id}_{patient.patient_name}_{patient.patient_disease}_{patient.patient_gender}_{patient.patient_age}\n")

class Management:
    def display_menu(self):
        doctor_manager = DoctorManager()
        patient_manager = PatientManager()

        while True:
            print("\nMain Menu:")
            print("1 - Doctors Menu")
            print("2 - Patients Menu")
            print("3 - Exit")
            choice = input(">>> ")

            if choice == "1":
                while True:
                    print("\nDoctors Menu:")
                    print("1 - Display Doctors List")
                    print("2 - Search Doctor by ID")
                    print("3 - Search Doctor by Name")
                    print("4 - Add Doctor")
                    print("5 - Edit Doctor Info")
                    print("6 - Back to Main Menu")
                    option = input(">>> ")

                    if option == "1":
                        doctor_manager.display_doctors_list()
                    elif option == "2":
                        doctor_manager.search_doctor_by_id()
                    elif option == "3":
                        doctor_manager.search_doctor_by_name()
                    elif option == "4":
                        doctor_manager.add_dr_to_file()
                    elif option == "5":
                        doctor_manager.edit_doctor_info()
                    elif option == "6":
                        break

            elif choice == "2":
                while True:
                    print("\nPatients Menu:")
                    print("1 - Display Patients List")
                    print("2 - Search for patient by ID")
                    print("3 - Add Patient")
                    print("4 - Edit patient info")
                    print("5 - Back to Main Menu")
                    option = input(">>> ")

                    if option == "1":
                        patient_manager.display_patients_list()
                    elif option == "2":
                        patient_manager.search_patient_by_id()
                    elif option == "3":
                        patient_manager.add_patient_to_file()
                    elif option == "4":
                        patient_manager.edit_patient_info()
                    elif option == "5":
                        break

            elif choice == "3":
                print("Thanks for using the program. Bye!")
                break


if __name__ == "__main__":
    management = Management()
    management.display_menu()
