def init_db():
    schema_sql = [
        """
        CREATE TABLE IF NOT EXISTS campus (
          campus_id SERIAL PRIMARY KEY,
          campus_name TEXT NOT NULL UNIQUE,
          location TEXT
        );
        """,
        """
        CREATE TABLE IF NOT EXISTS student (
          student_id SERIAL PRIMARY KEY,
          name TEXT NOT NULL,
          email TEXT UNIQUE,
          campus_id INT REFERENCES campus(campus_id)
        );
        """,
        """
        CREATE TABLE IF NOT EXISTS course (
          course_id SERIAL PRIMARY KEY,
          title TEXT UNIQUE,
          credits INT
        );
        """,
        """
        CREATE TABLE IF NOT EXISTS section (
          section_id SERIAL PRIMARY KEY,
          course_id INT REFERENCES course(course_id),
          term TEXT,
          campus_id INT REFERENCES campus(campus_id)
        );
        """,
        """
        CREATE TABLE IF NOT EXISTS enrollment (
          enroll_id SERIAL PRIMARY KEY,
          student_id INT REFERENCES student(student_id),
          section_id INT REFERENCES section(section_id),
          grade CHAR(2)
        );
        """
    ]

    sample_data_sql = [
        # --- Campuses ---
        "INSERT INTO campus (campus_name, location) VALUES ('Main Campus', 'New York') ON CONFLICT DO NOTHING;",
        "INSERT INTO campus (campus_name, location) VALUES ('South Campus', 'Texas') ON CONFLICT DO NOTHING;",
        "INSERT INTO campus (campus_name, location) VALUES ('West Campus', 'California') ON CONFLICT DO NOTHING;",
        "INSERT INTO campus (campus_name, location) VALUES ('North Campus', 'Chicago') ON CONFLICT DO NOTHING;",
        "INSERT INTO campus (campus_name, location) VALUES ('East Campus', 'Florida') ON CONFLICT DO NOTHING;",

        # --- Courses ---
        "INSERT INTO course (title, credits) VALUES ('Database Systems', 3) ON CONFLICT DO NOTHING;",
        "INSERT INTO course (title, credits) VALUES ('Computer Networks', 4) ON CONFLICT DO NOTHING;",
        "INSERT INTO course (title, credits) VALUES ('Algorithms', 3) ON CONFLICT DO NOTHING;",
        "INSERT INTO course (title, credits) VALUES ('Operating Systems', 4) ON CONFLICT DO NOTHING;",
        "INSERT INTO course (title, credits) VALUES ('Artificial Intelligence', 3) ON CONFLICT DO NOTHING;",
        "INSERT INTO course (title, credits) VALUES ('Machine Learning', 3) ON CONFLICT DO NOTHING;",
        "INSERT INTO course (title, credits) VALUES ('Cyber Security', 4) ON CONFLICT DO NOTHING;",
        "INSERT INTO course (title, credits) VALUES ('Data Mining', 3) ON CONFLICT DO NOTHING;",
        "INSERT INTO course (title, credits) VALUES ('Software Engineering', 4) ON CONFLICT DO NOTHING;",
        "INSERT INTO course (title, credits) VALUES ('Cloud Computing', 3) ON CONFLICT DO NOTHING;",

        # --- Students (25 total) ---
        "INSERT INTO student (name, email, campus_id) VALUES ('Alice Johnson', 'alice@example.com', 1) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Bob Smith', 'bob@example.com', 2) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Charlie Rao', 'charlie@example.com', 3) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Diana Lopez', 'diana@example.com', 1) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Ethan Brown', 'ethan@example.com', 2) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Fiona Zhang', 'fiona@example.com', 4) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('George Patel', 'george@example.com', 5) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Hannah Wilson', 'hannah@example.com', 3) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Ian Thomas', 'ian@example.com', 2) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Julia Kim', 'julia@example.com', 1) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Kevin White', 'kevin@example.com', 4) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Liam Davis', 'liam@example.com', 5) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Maya Singh', 'maya@example.com', 3) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Nathan Reed', 'nathan@example.com', 2) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Olivia Chen', 'olivia@example.com', 1) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Peter Kumar', 'peter@example.com', 4) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Quinn Lee', 'quinn@example.com', 5) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Rita Johnson', 'rita@example.com', 3) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Samir Ahmed', 'samir@example.com', 1) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Tina Moore', 'tina@example.com', 2) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Uma Reddy', 'uma@example.com', 4) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Victor Green', 'victor@example.com', 5) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Wendy Harris', 'wendy@example.com', 3) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Xavier Collins', 'xavier@example.com', 1) ON CONFLICT DO NOTHING;",
        "INSERT INTO student (name, email, campus_id) VALUES ('Yara Banerjee', 'yara@example.com', 2) ON CONFLICT DO NOTHING;",

        # --- Sections (10 total) ---
        "INSERT INTO section (course_id, term, campus_id) VALUES (1, 'Fall2025', 1) ON CONFLICT DO NOTHING;",
        "INSERT INTO section (course_id, term, campus_id) VALUES (2, 'Fall2025', 2) ON CONFLICT DO NOTHING;",
        "INSERT INTO section (course_id, term, campus_id) VALUES (3, 'Fall2025', 3) ON CONFLICT DO NOTHING;",
        "INSERT INTO section (course_id, term, campus_id) VALUES (4, 'Fall2025', 4) ON CONFLICT DO NOTHING;",
        "INSERT INTO section (course_id, term, campus_id) VALUES (5, 'Fall2025', 5) ON CONFLICT DO NOTHING;",
        "INSERT INTO section (course_id, term, campus_id) VALUES (6, 'Fall2025', 1) ON CONFLICT DO NOTHING;",
        "INSERT INTO section (course_id, term, campus_id) VALUES (7, 'Fall2025', 2) ON CONFLICT DO NOTHING;",
        "INSERT INTO section (course_id, term, campus_id) VALUES (8, 'Fall2025', 3) ON CONFLICT DO NOTHING;",
        "INSERT INTO section (course_id, term, campus_id) VALUES (9, 'Fall2025', 4) ON CONFLICT DO NOTHING;",
        "INSERT INTO section (course_id, term, campus_id) VALUES (10, 'Fall2025', 5) ON CONFLICT DO NOTHING;",

        # --- Enrollments (25) ---
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (1, 1, 'A') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (2, 2, 'B') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (3, 3, 'A') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (4, 4, 'B') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (5, 5, 'A') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (6, 6, 'C') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (7, 7, 'B') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (8, 8, 'A') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (9, 9, 'B') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (10, 10, 'A') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (11, 1, 'A') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (12, 2, 'B') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (13, 3, 'C') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (14, 4, 'A') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (15, 5, 'B') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (16, 6, 'A') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (17, 7, 'C') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (18, 8, 'A') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (19, 9, 'B') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (20, 10, 'A') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (21, 1, 'B') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (22, 2, 'A') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (23, 3, 'B') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (24, 4, 'C') ON CONFLICT DO NOTHING;",
        "INSERT INTO enrollment (student_id, section_id, grade) VALUES (25, 5, 'A') ON CONFLICT DO NOTHING;"
    ]

    conn = get_connection()
    cur = conn.cursor()
    
    for stmt in schema_sql:
        cur.execute(stmt)

    for stmt in sample_data_sql:
        cur.execute(stmt)

    conn.commit()
    cur.close()
    conn.close()
