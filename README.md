-class Symptom:
    def __init__(self, name):
        self.name = name

class Disease:
    def __init__(self, name):
        self.name = name
        self.symptoms = []

    def add_symptom(self, symptom):
        self.symptoms.append(symptom)

class Patient:
    def __init__(self, name):
        self.name = name
        self.symptoms = []

    def add_symptom(self, symptom):
        self.symptoms.append(symptom)

fever = Symptom("Fever")
cough = Symptom("Cough")
rash = Symptom("Rash")


symptom_knowledge_base = {
    "fever": fever,
    "cough": cough,
    "rash": rash
}

flu = Disease("Flu")
measles = Disease("Measles")

# Add Symptoms to Diseases
flu.add_symptom(fever)
flu.add_symptom(cough)
measles.add_symptom(rash)
measles.add_symptom(fever)

# Disease Knowledge Base
disease_knowledge_base = {
    "flu": flu,
    "measles": measles
}

def diagnose(patient):
    if fever in patient.symptoms and cough in patient.symptoms:
        return "Flu"
    elif rash in patient.symptoms and fever in patient.symptoms:
        return "Measles"
    else:
        return "Unknown Condition"

def get_user_symptoms():
    user_symptoms = []
    while True:
        symptom_input = input("Enter a symptom (or type 'done' to finish): ").lower()
        if symptom_input == 'done':
            break
        elif symptom_input in symptom_knowledge_base:
            user_symptoms.append(symptom_knowledge_base[symptom_input])
        else:
            print(f"Symptom '{symptom_input}' is not recognized. Please enter a valid symptom.")
    return user_symptoms

def main():
    patient_name = input("Enter the patient's name: ")
    patient = Patient(patient_name)

    print("Enter the symptoms the patient is experiencing:")
    patient.symptoms = get_user_symptoms()

    diagnosis = diagnose(patient)
    print(f"{patient.name}'s Diagnosis: {diagnosis}")

if __name__ == "__main__":
    main()
