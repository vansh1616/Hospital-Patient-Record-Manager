import uuid

class Patient:
    def _init_(self, name, age, gender, diagnosis):
        self.id = str(uuid.uuid4())[:8]  # Unique ID (shortened UUID)
        self.name = name
        self.age = age
        self.gender = gender
        self.diagnosis = diagnosis

    def _str_(self):
        return (f"ID: {self.id}\n"
                f"Name: {self.name}\n"
                f"Age: {self.age}\n"
                f"Gender: {self.gender}\n"
                f"Diagnosis: {self.diagnosis}\n")

class PatientManager:
    def _init_(self):
        self.patients = {}

    def create_patient(self, name, age, gender, diagnosis):
        patient = Patient(name, age, gender, diagnosis)
        self.patients[patient.id] = patient
        print(f"\n✅ Patient '{name}' added successfully with ID: {patient.id}")

    def read_patients(self):
        if not self.patients:
            print("\n📭 No patient records found.")
        else:
            print("\n📋 All Patient Records:")
            for patient in self.patients.values():
                print(patient)

    def update_patient(self, patient_id, name=None, age=None, gender=None, diagnosis=None):
        patient = self.patients.get(patient_id)
        if patient:
            if name:
                patient.name = name
            if age:
                patient.age = age
            if gender:
                patient.gender = gender
            if diagnosis:
                patient.diagnosis = diagnosis
            print(f"\n✏ Patient '{patient_id}' updated successfully.")
        else:
            print("\n❌ Patient ID not found.")

    def delete_patient(self, patient_id):
        if patient_id in self.patients:
            del self.patients[patient_id]
            print(f"\n🗑 Patient '{patient_id}' deleted successfully.")
        else:
            print("\n❌ Patient ID not found.")

def menu():
    manager = PatientManager()
    while True:
        print("\n====== Hospital Patient Record Manager ======")
        print("1. Add New Patient")
        print("2. View All Patients")
        print("3. Update Patient Record")
        print("4. Delete Patient Record")
        print("5. Exit")
        choice = input("Enter your choice (1-5): ")

        if choice == '1':
            name = input("Enter patient name: ")
            age = input("Enter patient age: ")
            gender = input("Enter patient gender: ")
            diagnosis = input("Enter diagnosis: ")
            manager.create_patient(name, age, gender, diagnosis)

        elif choice == '2':
            manager.read_patients()

        elif choice == '3':
            patient_id = input("Enter patient ID to update: ")
            print("Leave field blank to keep current value.")
            name = input("New name: ") or None
            age = input("New age: ") or None
            gender = input("New gender: ") or None
            diagnosis = input("New diagnosis: ") or None
            manager.update_patient(patient_id, name, age, gender, diagnosis)

        elif choice == '4':
            patient_id = input("Enter patient ID to delete: ")
            manager.delete_patient(patient_id)

        elif choice == '5':
            print("👋 Exiting the program.")
            break

        else:
            print("❗ Invalid choice. Please try again.")

if __name__  == "_main_":
    menu()
