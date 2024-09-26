import React, { useState, useContext } from 'react';
import { useNavigate } from 'react-router-dom';
import './MainPage.css';
import { UserContext } from './UserContext'; // UserContext를 import
import step1 from './img/step1.png';
import step2 from './img/step2.png';
import step3 from './img/step3.png';
import step4 from './img/step4.png';
import step5 from './img/step5.png';
import step6 from './img/step6.png';
import step7 from './img/step7.png';
import step8 from './img/step8.png';
import step9 from './img/step9.png';


const MainPage = () => {
  const navigate = useNavigate();
  const [sidebarOpen, setSidebarOpen] = useState(false);
  const { user } = useContext(UserContext); // UserContext에서 user 정보를 가져옵니다.
  const [currentStep, setCurrentStep] = useState(0); // 현재 페이지 인덱스 관리

  const steps = [
    {
    image: step1
    },
    {
    image: step2
    },
    {
      image: step3
    },
    {
      image: step4
    },
    {
      image: step5
    },
    {
      image: step6
    },
    {
      image: step7
    },
    {
      image: step8
    },
    {
      image: step9
    },

  ];

  const nextStep = () => {
    setCurrentStep((prevStep) => (prevStep + 1) % steps.length);
  };

  const prevStep = () => {
    setCurrentStep((prevStep) => (prevStep - 1 + steps.length) % steps.length);
  };

  const toggleSidebar = () => {
    setSidebarOpen(!sidebarOpen);
  };

  const handleLogout = () => {
    navigate('/login'); // Login.js로 이동
  };

  const handleGuidePage = () => {
    navigate('/Guide'); // Guide.js로 이동
  };

  const handleExpensePage = () => {
    navigate('/Expense'); // Expense.js로 이동
  };

  return (
    <div className="main-container">
      <div className="m-content-box">
        <header className="navbar">
          <div className="nav-left">
            <button className="nav-toggle" onClick={toggleSidebar}>&#9776;</button>
            <h4>업무 신청</h4>
          </div>
        </header>

        <div
          className="sidebar"
          style={{ width: sidebarOpen ? '220px' : '0' }} // 사이드바 폭 설정
        >
          <a href="#" className="closebtn" onClick={toggleSidebar}>&times;</a>

          <div className="sidebar-section">
            <div className="user-info">
              <h3>{user?.name || '이름 없음'} 님</h3> {/* UserContext에서 가져온 이름을 표시 */}
            </div>
          </div>

          <div className="sidebar-section">
            <h3>내 정보</h3>
            <a href="#" className="sidebar-link">업무 신청</a>
          </div>

          <div className="sidebar-section">
            <h3>업무 정보</h3>
            <a href="#" className="sidebar-link">체크리스트</a>
            <a href="#" className="sidebar-link">업무 정보</a>
            <a href="#" className="sidebar-link">이용 정보</a>
          </div>
          <div className="sidebar-section">
            <a href="#" className="sidebar-link" onClick={handleLogout}>로그아웃</a>
          </div>
        </div>
        <div
          className="overlay"
          style={{ display: sidebarOpen ? 'block' : 'none' }}
          onClick={toggleSidebar}
        ></div>

        <div className="task-section">
          <button className="task-button" onClick={() => navigate('/Residence')}>
            + 업무 신청
          </button>
        </div>
        <div className="method-expense-container">
          <button className="method-box" onClick={handleGuidePage}>이용 방법</button> {/* 이용 방법 버튼 클릭 시 Guide.js로 이동 */}
          <button className="expense-box" onClick={handleExpensePage}>서비스 요금</button>
        </div>

        <div className="layout-container">
          {/* Step 박스 (왼쪽 섹션) */}
          <div className="step-box">
            <button className="prev-button" onClick={prevStep}>←</button>
            <div className="step-content">
              <img src={steps[currentStep].image} alt={`Step ${currentStep + 1}`} className="step-image" />
              <p>{steps[currentStep].description}</p>
            </div>
            <button className="next-button" onClick={nextStep}>→</button>
            <div className="step-indicator">
              {steps.map((_, index) => (
                <span
                  key={index}
                  className={`dot ${currentStep === index ? 'active' : ''}`}
                ></span>
              ))}
            </div>
          </div>

          {/* History 박스 (오른쪽 섹션) */}
          <div className="history-box">
            <p>HISTORY 박스입니다.</p>
          </div>
        </div>
      </div>
    </div>
  );
};

export default MainPage;
