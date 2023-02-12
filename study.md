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


3. useParams란?
useParams는 리액트에서 제공하는 Hook으로 동적으로 라우팅을 생성하기 위해 사용한다.

URL에 포함되어있는 Key, Value 형식의 객체를 반환해주는 역할을 한다. Route 부분에서 Key를 지정해주고, 해당하는 Key에 적합한 Value를 넣어 URL을 변경시키면, useParams를 통해 Key, Value 객체를 반환받아 확인할 수 있다. 반환받은 Value를 통해 게시글을 불러오거나, 검색목록을 변경시키는 등 다양한 기능으로 확장시켜 사용할 수 있다.

    1) useParams에 전달하는 값은 path에서 : 콜론으로 시작한다.
        <Route path=":courseSlug" element={<CoursePage />}/>

    2) CoursePage 컴포넌트에서 useParams를 import 한뒤 hook 호출
        import { useParams } from 'react-router-dom';
        const { courseSlug } = useParams(); 

    3) courseSlug라는 변수명으로 할당된 값을 사용
          const course = getCourseBySlug(courseSlug);
 