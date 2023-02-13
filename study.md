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
 

 4. 특정 조건일때 다른 페이지로 이동하게(redirect) 해주는 Navigate
   if (!question) {
    return <Navigate to="/questions" />
  }


5. useSearchParams(); = 리액트에서 query parameter 값을 가져오기 위해 제공되는 커스텀 hook

    useState의 형식으로 사용
  const [searchParams, setSearchParams] = useSearchParams();

     searchParams.get으로 parameter를 가져올 수 있음
  const initKeyword = searchParams.get('keyword')

6. useNavigate(); = 페이지를 코드를 사용해서 이용할때 사용하는 커스텀 hook

const navigate = useNavigate();

navigate('/wishlist');


7. Link, Navigate, useNavigate는 언제 쓰는게 좋을까?
세 가지 모두 다 페이지를 이동할 때 쓸 수 있다는 점에서 비슷한데요.

이것들을 언제 사용하면 좋을지 예시랑 같이 한번 살펴봅시다.

Link
사용자가 클릭해서 페이지를 이동하도록 할 때 사용하면 됩니다.

하이퍼링크 텍스트나 페이지를 이동하는 버튼, 이미지 등에 사용하면 되겠죠?

대부분의 경우 Link 만으로도 충분합니다.

Navigate
특정 경로에서 렌더링 시점에 다른 페이지로 이동시키고 싶을 때 사용하면 됩니다.

예시:

쇼핑몰의 회원 전용 페이지에 로그인없이 들어와서 로그인 페이지로 리다이렉트하는 경우
쇼핑몰의 상품 상세 페이지에서 제품이 품절되었거나 삭제되어서 다른 페이지로 이동시키는 경우
useNavigate
특정한 코드의 실행이 끝나고 나서 페이지를 이동시키고 싶을 때 사용하면 됩니다.

예시:

쇼핑몰에서 장바구니에 담기를 눌렀을 때 리퀘스트를 보내고 장바구니 페이지로 이동시키는 경우
쇼핑몰에서 결제하기 버튼을 누르고 나서 모든 결제가 완료된 후에 페이지를 이동시키는 경우
리다이렉트된 로그인 페이지에서 로그인을 완료한 후에 처음 진입했던 페이지로 돌아가는 경우