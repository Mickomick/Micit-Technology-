<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>MICIT Technology - Student Registration Portal</title>
  <style>
    :root {
      --primary: #1e3a8a;
      --primary-hover: #1d4ed8;
      --bg: #f3f4f6;
      --card-bg: #ffffff;
      --text: #1f2937;
      --border: #d1d5db;
      --error: #dc2626;
      --success: #16a34a;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    body {
      background-color: var(--bg);
      color: var(--text);
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      padding: 20px;
    }

    .container {
      background-color: var(--card-bg);
      width: 100%;
      max-width: 500px;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
    }

    .header {
      text-align: center;
      margin-bottom: 24px;
    }

    .header h1 {
      color: var(--primary);
      font-size: 1.5rem;
      letter-spacing: 0.5px;
      margin-bottom: 6px;
    }

    .header p {
      color: #6b7280;
      font-size: 0.9rem;
    }

    .form-group {
      margin-bottom: 16px;
    }

    label {
      display: block;
      font-size: 0.875rem;
      font-weight: 600;
      margin-bottom: 6px;
    }

    input, select {
      width: 100%;
      padding: 10px 12px;
      border: 1px solid var(--border);
      border-radius: 6px;
      font-size: 0.95rem;
      outline: none;
      transition: border-color 0.2s ease;
    }

    input:focus, select:focus {
      border-color: var(--primary);
      box-shadow: 0 0 0 3px rgba(30, 58, 138, 0.1);
    }

    .error-msg {
      color: var(--error);
      font-size: 0.775rem;
      margin-top: 4px;
      display: none;
    }

    .btn-group {
      display: flex;
      gap: 12px;
      margin-top: 20px;
    }

    button {
      flex: 1;
      padding: 12px;
      border: none;
      border-radius: 6px;
      font-size: 0.95rem;
      font-weight: 600;
      cursor: pointer;
      transition: background-color 0.2s ease;
    }

    .btn-submit {
      background-color: var(--primary);
      color: white;
    }

    .btn-submit:hover {
      background-color: var(--primary-hover);
    }

    .btn-clear {
      background-color: #e5e7eb;
      color: var(--text);
    }

    .btn-clear:hover {
      background-color: #d1d5db;
    }

    .status-banner {
      margin-top: 20px;
      padding: 12px;
      border-radius: 6px;
      font-size: 0.875rem;
      display: none;
      text-align: center;
    }

    .status-banner.success {
      background-color: #dcfce7;
      color: var(--success);
      border: 1px solid #bbf7d0;
    }

    .status-banner.error {
      background-color: #fee2e2;
      color: var(--error);
      border: 1px solid #fecaca;
    }
  </style>
</head>
<body>

  <div class="container">
    <div class="header">
      <h1>MICIT TECHNOLOGY</h1>
      <p>Student Registration Submission Portal</p>
    </div>

    <form id="registrationForm" novalidate>
      <div class="form-group">
        <label for="fullName">Full Name</label>
        <input type="text" id="fullName" placeholder="John Doe">
        <div class="error-msg" id="fullNameError">Full Name is required.</div>
      </div>

      <div class="form-group">
        <label for="email">Email Address</label>
        <input type="email" id="email" placeholder="student@example.com">
        <div class="error-msg" id="emailError">Please enter a valid email address.</div>
      </div>

      <div class="form-group">
        <label for="phone">Phone Number</label>
        <input type="tel" id="phone" placeholder="08012345678">
        <div class="error-msg" id="phoneError">Please enter a valid phone number (digits only).</div>
      </div>

      <div class="form-group">
        <label for="dob">Date of Birth</label>
        <input type="date" id="dob">
        <div class="error-msg" id="dobError">Please select your date of birth.</div>
      </div>

      <div class="form-group">
        <label for="gender">Gender</label>
        <select id="gender">
          <option value="">Select Gender</option>
          <option value="Male">Male</option>
          <option value="Female">Female</option>
          <option value="Other">Other</option>
        </select>
        <div class="error-msg" id="genderError">Please select a gender.</div>
      </div>

      <div class="form-group">
        <label for="course">Course of Study</label>
        <select id="course">
          <option value="">Select Course</option>
          <option value="Software Engineering">Software Engineering</option>
          <option value="Data Science & AI">Data Science & AI</option>
          <option value="Cyber Security">Cyber Security</option>
          <option value="Web Development">Web Development</option>
          <option value="UI/UX Design">UI/UX Design</option>
        </select>
        <div class="error-msg" id="courseError">Please select a course.</div>
      </div>

      <div class="btn-group">
        <button type="submit" class="btn-submit">Submit Registration</button>
        <button type="button" class="btn-clear" id="clearBtn">Clear</button>
      </div>
    </form>

    <div class="status-banner" id="statusBanner"></div>
  </div>

  <script>
    const form = document.getElementById('registrationForm');
    const clearBtn = document.getElementById('clearBtn');
    const statusBanner = document.getElementById('statusBanner');

    const fields = {
      fullName: document.getElementById('fullName'),
      email: document.getElementById('email'),
      phone: document.getElementById('phone'),
      dob: document.getElementById('dob'),
      gender: document.getElementById('gender'),
      course: document.getElementById('course')
    };

    const errors = {
      fullName: document.getElementById('fullNameError'),
      email: document.getElementById('emailError'),
      phone: document.getElementById('phoneError'),
      dob: document.getElementById('dobError'),
      gender: document.getElementById('genderError'),
      course: document.getElementById('courseError')
    };

    // Validation patterns
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    const phoneRegex = /^[0-9]{8,15}$/;

    function validate() {
      let isValid = true;

      // Reset error displays
      Object.keys(errors).forEach(key => errors[key].style.display = 'none');

      if (!fields.fullName.value.trim()) {
        errors.fullName.style.display = 'block';
        isValid = false;
      }

      if (!emailRegex.test(fields.email.value.trim())) {
        errors.email.style.display = 'block';
        isValid = false;
      }

      if (!phoneRegex.test(fields.phone.value.trim())) {
        errors.phone.style.display = 'block';
        isValid = false;
      }

      if (!fields.dob.value) {
        errors.dob.style.display = 'block';
        isValid = false;
      }

      if (!fields.gender.value) {
        errors.gender.style.display = 'block';
        isValid = false;
      }

      if (!fields.course.value) {
        errors.course.style.display = 'block';
        isValid = false;
      }

      return isValid;
    }

    form.addEventListener('submit', function (e) {
      e.preventDefault();

      if (!validate()) {
        showStatus('Please correct the highlighted errors in the form.', 'error');
        return;
      }

      const regId = 'MICIT-' + Math.floor(10000 + Math.random() * 90000);
      const data = {
        regId: regId,
        fullName: fields.fullName.value.trim(),
        email: fields.email.value.trim(),
        phone: fields.phone.value.trim(),
        dob: fields.dob.value,
        gender: fields.gender.value,
        course: fields.course.value,
        dateSubmitted: new Date().toISOString().split('T')[0]
      };

      // 1. Format Datasheet Content
      const datasheetContent = 
`==========================================
      MICIT TECHNOLOGY REGISTRATION
==========================================
Registration ID : ${data.regId}
Full Name       : ${data.fullName}
Email Address   : ${data.email}
Phone Number    : ${data.phone}
Date of Birth   : ${data.dob}
Gender          : ${data.gender}
Selected Course : ${data.course}
Submission Date : ${data.dateSubmitted}
==========================================`;

      // 2. Automatically Download Local Datasheet File
      downloadDatasheet(`Datasheet_${data.regId}.txt`, datasheetContent);

      // 3. Open Mail App to Send to target email
      const targetEmail = 'micittechnology@gmail.com';
      const subject = encodeURIComponent(`New Student Registration - ${data.fullName} (${data.regId})`);
      const body = encodeURIComponent(`Please find the registration details attached below:\n\n${datasheetContent}\n\nNote: Please attach the downloaded file "Datasheet_${data.regId}.txt" if required.`);
      
      window.location.href = `mailto:${targetEmail}?subject=${subject}&body=${body}`;

      showStatus(`Registration submitted! Datasheet saved locally. Please send the pre-filled email to ${targetEmail}.`, 'success');
    });

    function downloadDatasheet(filename, text) {
      const blob = new Blob([text], { type: 'text/plain' });
      const link = document.createElement('a');
      link.href = URL.createObjectURL(blob);
      link.download = filename;
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
      URL.revokeObjectURL(link.href);
    }

    clearBtn.addEventListener('click', function () {
      form.reset();
      Object.keys(errors).forEach(key => errors[key].style.display = 'none');
      statusBanner.style.display = 'none';
    });

    function showStatus(msg, type) {
      statusBanner.textContent = msg;
      statusBanner.className = `status-banner ${type}`;
      statusBanner.style.display = 'block';
    }
  </script>
</body>
</html>
