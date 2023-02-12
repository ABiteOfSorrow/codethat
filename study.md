1. "react-router-dom": "^6.8.1", 설치

ex) 사용 형식
     <BrowserRouter>
            <Routes>
                <Route path="/" element={<App />}>
                <Route index element={<HomePage />} />
                    <Route path="courses">
                        <Route index element={<CourseListPage />} />                
                        <Route path="react-frontend-development" element={<CoursePage />}/>
                    </Route>
                <Route path="wishList" element={<WishlistPage />} />
                <Route path="questions" element={<QuestionListPage/ >} />
                <Route path="questions/616825" element={<QuestionPage/ >} />
                </Route>
                <Link to={`/questions/${question.id}`}>{question.title}</Link>
            </Routes>
    </BrowserRouter>


2. Route안에 Route를 사용하는 중첩 routing 방식이 있다.
    이때 Routes안에는 Route나 fragment만 사용할 수 있기 때문에
    
main.js -
    <Route path="/" element={<App />}>

App.js -
    function App() {
         return (
    <>
      <Nav className={styles.nav} />
      <div className={styles.body}><Outlet /></div>
      <Footer className={styles.footer} />
    </>
  );
}

공통된 요소를 route와 충돌 없이 사용하고 싶으면  children 대신 리액트에서 제공하는 <Outlet /> 컴포넌트를 사용한다.