This post will be about Phase2 Project using the React.

I planed to build Workout recording app. In this app, I wanted users to be registered by username, and when they sign in, they access thier page as "My Page". They can plan or record their routine.

So, What I needed to build are Router, some of component.

At the First, I created some js files as basic component. These are about Header, Home, NavBar, SignUp, SignIn, MyPage. User can access other pages using NavBar with Router.

```
      <Header/>
      <Router>
        <Routes>
          <Route path="/" element={<NavBar/>}>
            <Route index element={<Home/>}/>
            <Route path="/signup" element={<SignUp/>}/>
            <Route path="/signin" element={<SignIn/>}/>
          </Route>
          <Route path=":username/mypage" element={<MyPage/>}/>
        </Routes>
      </Router>
```

I wanted to build form. Name, username and password are required. And also there are some requirement when users register:

```
        const firstNamePattern = /^[a-zA-Z]+$/;
        const usernamePattern = /^[a-z0-9]{8,}$/;
        const passwordPattern = /^\d{4,}$/;
        
        if (!firstNamePattern.test(formData.firstname)) {
            alert("First name should contain only alphabets.");
            return;
          }
    
        if (!usernamePattern.test(formData.username)) {
            alert("Username should be at least 8 lowercase letters or digits.");
            return;
        }

        if (!passwordPattern.test(formData.password)) {
            alert("Password should be at least 4 digits.");
            return;
        }
```

Using regex, User keep these conditions, first name should contain only alphabets, username sould be at least 8 lowercase letters or digits, and password sould be at least 4 digits.

To sign in, I wanted to match username and form data.

```
fetch("http://localhost:3000/users")
        .then((response) => response.json())
        .then((data) => {
        const user = data.find((user) => user.username === formData.username);
        if (user && user.password === formData.password) {
            localStorage.setItem("firstname", user.firstname);
            localStorage.setItem("id", user.id);
            navigate(`/${formData.username}/mypage`);
        } else {
            alert("You put the wrong username or password. Try again.");
        }
        })
        .catch((error) => {
        console.error("Error:", error);
        });
```

If form data matches from username and password in json file, users can access their 'My Page'. So I used useNavigate hook.

At 'My Page' I put the Calendar by date picker react library. the form is for record workout. If there is recorded data, this data will be rendered.

```
  const handleSubmit = (e) => {
    e.preventDefault();

    if (selectedDate && exerciseRecord) {
      const newRecord = { date: selectedDate.toLocaleDateString(), record: exerciseRecord };

      if (userData) {
        let updatedRecords = [];

        if (userData.records) {
          const dateIndex = userData.records.findIndex((item) => item.date === newRecord.date);

          if (dateIndex === -1) {
            // if there is no record for selected date, create a new one
            updatedRecords = [...userData.records, { date: newRecord.date, record: [newRecord.record] }];
          } else {
            // if there is already a record for selected date, add a new record
            updatedRecords = [...userData.records];
            const dateRecord = updatedRecords[dateIndex];
            const updatedDateRecord = {
              ...dateRecord,
              record: [...dateRecord.record, newRecord.record]
            };
            updatedRecords[dateIndex] = updatedDateRecord;
          }
        } else {
          // if userData does not have records, create a new record
          updatedRecords = [{ date: newRecord.date, record: [newRecord.record] }];
        }

        const newData = { ...userData, records: updatedRecords };
        setUserData(newData);
        saveDataToServer(newData);
        console.log(`Exercise record saved for ${userId}`);
      }
    }
  };

  const saveDataToServer = (data) => {
    fetch(`http://localhost:3000/users/${userId}`, {
      method: "PATCH",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(data),
    })
      .then((response) => response.json())
      .then((data) => console.log(data))
      .catch((error) => console.error(error));
  };
```

When submit this form, handleSubmit is excuted. There are some conditions. The reason why I overlapped the conditional statement is patch the data more axactly.

This is json file. Submitted datas from form are saved at each date. And each workout data contain delete button to remove each workout data from json file.
```
{
      "firstname": "Yehwan",
      "username": "yehwan123",
      "password": "1234",
      "id": 1,
      "records": [
        {
          "date": "28/04/2023",
          "record": [
            {
              "workout": "pullup",
              "reps": "5",
              "sets": "5"
            }
          ]
        },
        {
          "date": "29/04/2023",
          "record": [
            {
              "workout": "Bench Press",
              "reps": "5",
              "sets": "5"
            },
            {
              "workout": "Dips",
              "reps": "5",
              "sets": "5"
            }
          ]
        }
      ]
    }
```

Sadly, This project is very challenging to me. I'm still having difficulty with writing code using React. I was so stressed when this app didn't work I wanted it to. But in this time, tried to use some react library and to be more familier with React. And I believe that I will improve my skill in using React.