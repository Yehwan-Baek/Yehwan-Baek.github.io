This post will be about Phase2 Project using the React.

I planed to build Workout recording app. In this app, I wanted users to be registered by username, and when they sign in, they access thier page as "My Page". They can plan or record their routine.

So, What I needed to build are Router, some of component.

At the First, I created some js files as basic component. These are about Home, NavBar, SignUp, SignIn, MyPage. User can access other pages using NavBar with Router.

```<Router>
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