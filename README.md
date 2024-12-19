# Resume-generator-
import fpdf

# Ask for user details
name = input("Enter your name: ")
email = input("Enter your email: ")
phone = input("Enter your phone number: ")

# Ask for objective
objective = input("Enter your career objective: ")

# Ask for education details
num_education = int(input("Enter the number of education entries: "))
education = []
for i in range(num_education):
    degree = input("Enter degree #{}: ".format(i+1))
    university = input("Enter university #{}: ".format(i+1))
    duration = input("Enter duration #{} (e.g., 2018-2022): ".format(i+1))
    education.append({"degree": degree, "university": university, "duration": duration})

# Ask for work experience details
num_work_experience = int(input("Enter the number of work experience entries: "))
work_experience = []
for i in range(num_work_experience):
    company = input("Enter company #{}: ".format(i+1))
    position = input("Enter position #{}: ".format(i+1))
    duration = input("Enter duration #{} (e.g., 2020-2022): ".format(i+1))
    num_achievements = int(input("Enter the number of achievements for #{}: ".format(i+1)))
    achievements = []
    for j in range(num_achievements):
        achievement = input("Enter achievement #{} for {}: ".format(j+1, company))
        achievements.append(achievement)
    work_experience.append({"company": company, "position": position, "duration": duration, "achievements": achievements})

# Ask for skills
num_skills = int(input("Enter the number of skills: "))
skills = []
for i in range(num_skills):
    skill = input("Enter skill #{}: ".format(i+1))
    skills.append(skill)

# Create a PDF object
pdf = fpdf.FPDF()

# Add a page
pdf.add_page()

# Set font and font size
pdf.set_font("Arial", size = 15)

# Add name and contact information
pdf.cell(200, 10, txt = name, ln = True, align = 'C')
pdf.ln(10)
pdf.set_font("Arial", size = 12)
pdf.cell(200, 10, txt = "Email: " + email, ln = True, align = 'L')
pdf.cell(200, 10, txt = "Phone: " + phone, ln = True, align = 'L')

# Add objective
pdf.ln(10)
pdf.set_font("Arial", size = 12, style = 'B')
pdf.cell(200, 10, txt = "Objective:", ln = True, align = 'L')
pdf.set_font("Arial", size = 12)
pdf.multi_cell(200, 10, txt = objective, align = 'L')

# Add education
pdf.ln(10)
pdf.set_font("Arial", size = 12, style = 'B')
pdf.cell(200, 10, txt = "Education:", ln = True, align = 'L')
for edu in education:
    pdf.set_font("Arial", size = 12)
    pdf.cell(200, 10, txt = edu["degree"] + ", " + edu["university"] + ", " + edu["duration"], ln = True, align = 'L')

# Add work experience
pdf.ln(10)
pdf.set_font("Arial", size = 12, style = 'B')
pdf.cell(200, 10, txt = "Work Experience:", ln = True, align = 'L')
for work in work_experience:
    pdf.set_font("Arial", size = 12)
    pdf.cell(200, 10, txt = work["company"] + ", " + work["position"] + ", " + work["duration"], ln = True, align = 'L')
    for achievement in work["achievements"]:
        pdf.cell(200, 10, txt = "- " + achievement, ln = True, align = 'L')

# Add skills
pdf.ln(10)
pdf.set_font("Arial", size = 12, style = 'B')
pdf.cell(200, 10, txt = "Skills:", ln = True, align = 'L')
pdf.set_font("Arial", size = 12)
pdf.cell(200, 10, txt = ", ".join(skills), ln = True, align = 'L')

# Save the PDF
pdf.output("resume.pdf")

print("Resume PDF saved as 'resume.pdf'")
