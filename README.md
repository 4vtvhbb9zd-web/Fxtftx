# Fxtftx
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام الاختبارات التفاعلي</title>
    <style>
        body {
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            color: #333;
            line-height: 1.6;
            padding: 20px;
            min-height: 100vh;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background-color: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            overflow: hidden;
        }
        
        header {
            background: linear-gradient(90deg, #2c3e50, #4a6491);
            color: white;
            padding: 25px;
            text-align: center;
            border-bottom: 5px solid #3498db;
        }
        
        h1 {
            font-size: 2.2rem;
            margin-bottom: 10px;
        }
        
        .subtitle {
            font-size: 1.2rem;
            opacity: 0.9;
        }
        
        .content {
            display: flex;
            flex-wrap: wrap;
        }
        
        .video-section {
            flex: 1;
            min-width: 300px;
            padding: 20px;
            background-color: #f8f9fa;
            border-left: 1px solid #e0e0e0;
        }
        
        .quiz-section {
            flex: 2;
            min-width: 300px;
            padding: 20px;
        }
        
        .video-container {
            background: #2c3e50;
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 20px;
            color: white;
            text-align: center;
        }
        
        .video-wrapper {
            position: relative;
            padding-bottom: 56.25%; /* 16:9 aspect ratio */
            height: 0;
            overflow: hidden;
            border-radius: 8px;
            margin: 15px 0;
        }
        
        .video-wrapper iframe {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border: none;
        }
        
        .lesson-content {
            background: white;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
            margin-top: 15px;
        }
        
        .question {
            background: white;
            padding: 20px;
            margin-bottom: 20px;
            border-radius: 10px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
            display: none;
        }
        
        .question.active {
            display: block;
        }
        
        .question-number {
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 10px;
            font-size: 1.1rem;
        }
        
        .question-text {
            font-size: 1.1rem;
            margin-bottom: 20px;
            color: #2c3e50;
        }
        
        .options {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        
        .option {
            padding: 12px 15px;
            background: #f8f9fa;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .option:hover {
            background: #e9ecef;
            border-color: #3498db;
        }
        
        .option.correct {
            background: #d4edda;
            border-color: #28a745;
            color: #155724;
        }
        
        .option.incorrect {
            background: #f8d7da;
            border-color: #dc3545;
            color: #721c24;
        }
        
        .explanation {
            margin-top: 15px;
            padding: 15px;
            border-radius: 8px;
            display: none;
        }
        
        .explanation.correct {
            background: #d4edda;
            border-left: 5px solid #28a745;
            display: block;
        }
        
        .explanation.incorrect {
            background: #f8d7da;
            border-left: 5px solid #dc3545;
            display: block;
        }
        
        .navigation {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
        }
        
        button {
            padding: 12px 25px;
            background: #3498db;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1rem;
            transition: background 0.3s;
        }
        
        button:hover {
            background: #2980b9;
        }
        
        button:disabled {
            background: #bdc3c7;
            cursor: not-allowed;
        }
        
        .results {
            text-align: center;
            padding: 30px;
            display: none;
        }
        
        .results.active {
            display: block;
        }
        
        .score {
            font-size: 2.5rem;
            font-weight: bold;
            color: #2c3e50;
            margin: 20px 0;
        }
        
        .percentage {
            font-size: 1.5rem;
            color: #3498db;
            margin-bottom: 20px;
        }
        
        .progress-bar {
            height: 10px;
            background: #e0e0e0;
            border-radius: 5px;
            margin: 20px 0;
            overflow: hidden;
        }
        
        .progress {
            height: 100%;
            background: #3498db;
            width: 0%;
            transition: width 0.5s;
        }
        
        .summary {
            margin-top: 20px;
            text-align: right;
        }
        
        .retry-btn {
            background: #2ecc71;
            margin-top: 20px;
        }
        
        .retry-btn:hover {
            background: #27ae60;
        }
        
        .student-grade {
            margin: 25px 0;
            padding: 20px;
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .grade-circle {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            background: #3498db;
            margin: 0 auto;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 2.5rem;
            font-weight: bold;
            box-shadow: 0 5px 15px rgba(52, 152, 219, 0.4);
        }
        
        .grade-text {
            margin-top: 15px;
            font-size: 1.3rem;
            color: #2c3e50;
            font-weight: bold;
        }
        
        .student-info {
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            margin-bottom: 20px;
            text-align: center;
        }
        
        .student-info h2 {
            color: #2c3e50;
            margin-bottom: 20px;
        }
        
        .form-group {
            margin-bottom: 20px;
            text-align: right;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .form-group select {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.3s;
        }
        
        .form-group select:focus {
            border-color: #3498db;
            outline: none;
        }
        
        .start-btn {
            background: #2ecc71;
            font-size: 1.2rem;
            padding: 15px 40px;
        }
        
        .start-btn:hover {
            background: #27ae60;
        }
        
        .student-details {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            text-align: center;
            border-right: 5px solid #3498db;
        }
        
        .student-details h3 {
            color: #2c3e50;
            margin-bottom: 10px;
        }
        
        .final-percentage {
            font-size: 3rem;
            font-weight: bold;
            color: #2c3e50;
            margin: 20px 0;
            text-align: center;
        }
        
        .final-grade {
            font-size: 2rem;
            color: #3498db;
            margin-bottom: 20px;
            text-align: center;
        }
        
        /* دوائر التقدم */
        .progress-indicators {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-bottom: 20px;
            justify-content: center;
        }
        
        .progress-indicator {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            background-color: #e0e0e0;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.8rem;
            font-weight: bold;
            color: #555;
            transition: all 0.3s;
        }
        
        .progress-indicator.current {
            background-color: #3498db;
            color: white;
            transform: scale(1.1);
        }
        
        .progress-indicator.correct {
            background-color: #28a745;
            color: white;
        }
        
        .progress-indicator.incorrect {
            background-color: #dc3545;
            color: white;
        }
        
        @media (max-width: 768px) {
            .content {
                flex-direction: column;
            }
            
            .video-section {
                border-left: none;
                border-bottom: 1px solid #e0e0e0;
            }
            
            .grade-circle {
                width: 120px;
                height: 120px;
                font-size: 2rem;
            }
            
            .final-percentage {
                font-size: 2.5rem;
            }
            
            .final-grade {
                font-size: 1.5rem;
            }
            
            .progress-indicators {
                gap: 5px;
            }
            
            .progress-indicator {
                width: 25px;
                height: 25px;
                font-size: 0.7rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>نظام الاختبارات التفاعلي</h1>
            <div class="subtitle">اختبار معرفي شامل - 50 سؤال</div>
        </header>
        
        <div class="content">
            <div class="quiz-section">
                <!-- قسم معلومات الطالب -->
                <div class="student-info" id="studentInfo">
                    <h2>بيانات الطالب</h2>
                    <div class="form-group">
                        <label for="studentName">الاسم الكامل</label>
                        <input type="text" id="studentName" placeholder="أدخل اسمك الكامل">
                    </div>
                    <div class="form-group">
                        <label for="section">الشعبة</label>
                        <select id="section">
                            <option value="">اختر الشعبة</option>
                            <option value="1">الشعبة 1</option>
                            <option value="2">الشعبة 2</option>
                            <option value="3">الشعبة 3</option>
                            <option value="4">الشعبة 4</option>
                            <option value="5">الشعبة 5</option>
                            <option value="6">الشعبة 6</option>
                            <option value="7">الشعبة 7</option>
                        </select>
                    </div>
                    <button class="start-btn" id="startBtn">بدء الاختبار</button>
                </div>
                
                <!-- دوائر التقدم -->
                <div class="progress-indicators" id="progressIndicators" style="display: none;"></div>
                
                <!-- قسم الأسئلة -->
                <div id="quizContainer" style="display: none;">
                    <div class="question active" id="question1">
                        <div class="question-number">السؤال 1 من 50</div>
                        <div class="question-text">ما هي عاصمة المملكة العربية السعودية؟</div>
                        <div class="options">
                            <div class="option" data-correct="true">الرياض</div>
                            <div class="option">جدة</div>
                            <div class="option">مكة المكرمة</div>
                            <div class="option">الدمام</div>
                        </div>
                        <div class="explanation"></div>
                        <div class="navigation">
                            <button id="nextBtn1" disabled>التالي</button>
                        </div>
                    </div>
                    
                    <div class="question" id="question2">
                        <div class="question-number">السؤال 2 من 50</div>
                        <div class="question-text">ما هو الكوكب الأقرب إلى الشمس؟</div>
                        <div class="options">
                            <div class="option">الزهرة</div>
                            <div class="option" data-correct="true">عطارد</div>
                            <div class="option">المريخ</div>
                            <div class="option">الأرض</div>
                        </div>
                        <div class="explanation"></div>
                        <div class="navigation">
                            <button id="nextBtn2" disabled>التالي</button>
                        </div>
                    </div>
                    
                    <!-- باقي الأسئلة (يمكن إضافة المزيد) -->
                    
                    <div class="question" id="question50">
                        <div class="question-number">السؤال 50 من 50</div>
                        <div class="question-text">ما هو العنصر الكيميائي الذي رمزه "O"؟</div>
                        <div class="options">
                            <div class="option">ذهب</div>
                            <div class="option">فضة</div>
                            <div class="option" data-correct="true">أكسجين</div>
                            <div class="option">أوزميوم</div>
                        </div>
                        <div class="explanation"></div>
                        <div class="navigation">
                            <button id="nextBtn50" disabled>إنهاء الاختبار</button>
                        </div>
                    </div>
                </div>
                
                <!-- قسم النتائج -->
                <div class="results" id="results">
                    <div class="student-grade">
                        <div class="grade-circle" id="gradeCircle">0%</div>
                        <div class="grade-text" id="gradeText">نتيجتك</div>
                    </div>
                    
                    <div class="final-percentage" id="finalPercentage">0%</div>
                    <div class="final-grade" id="finalGrade">تقدير: غير محدد</div>
                    
                    <div class="student-details">
                        <h3>معلومات الطالب</h3>
                        <p><strong>الاسم:</strong> <span id="resultName"></span></p>
                        <p><strong>الشعبة:</strong> <span id="resultSection"></span></p>
                    </div>
                    
                    <div class="summary">
                        <p>تهانينا! لقد أكملت الاختبار بنجاح.</p>
                        <p>سيتم إعادة تحميل الصفحة تلقائياً خلال <span id="countdown">10</span> ثوانٍ</p>
                    </div>
                </div>
            </div>
            
            <div class="video-section">
                <div class="video-container">
                    <h3>فيديو تعليمي</h3>
                    <div class="video-wrapper">
                        <!-- يمكن إضافة فيديو هنا -->
                        <div style="display: flex; align-items: center; justify-content: center; height: 100%; background: #1a2530; color: white; border-radius: 8px;">
                            <p>مساحة الفيديو التعليمي</p>
                        </div>
                    </div>
                    <p>شاهد هذا الفيديو للاستعداد للاختبار</p>
                </div>
                
                <div class="lesson-content">
                    <h3>معلومات إضافية</h3>
                    <p>هذا الاختبار يتكون من 50 سؤالاً متنوعاً في مجالات مختلفة.</p>
                    <p>يجب الإجابة على جميع الأسئلة ولا يمكنك الرجوع إلى السؤال السابق.</p>
                    <p>سيتم عرض نتيجتك فور الانتهاء من الإجابة على السؤال الأخير.</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // عناصر DOM
            const studentInfo = document.getElementById('studentInfo');
            const progressIndicators = document.getElementById('progressIndicators');
            const quizContainer = document.getElementById('quizContainer');
            const results = document.getElementById('results');
            const startBtn = document.getElementById('startBtn');
            const studentNameInput = document.getElementById('studentName');
            const sectionSelect = document.getElementById('section');
            const resultName = document.getElementById('resultName');
            const resultSection = document.getElementById('resultSection');
            const finalPercentage = document.getElementById('finalPercentage');
            const finalGrade = document.getElementById('finalGrade');
            const gradeCircle = document.getElementById('gradeCircle');
            const countdownElement = document.getElementById('countdown');
            
            // متغيرات التطبيق
            let currentQuestion = 1;
            let totalQuestions = 50;
            let score = 0;
            let answeredQuestions = 0;
            let userAnswers = {};
            let countdown;
            
            // إنشاء دوائر التقدم
            function createProgressIndicators() {
                progressIndicators.innerHTML = '';
                for (let i = 1; i <= totalQuestions; i++) {
                    const indicator = document.createElement('div');
                    indicator.className = 'progress-indicator';
                    indicator.textContent = i;
                    indicator.id = `indicator${i}`;
                    progressIndicators.appendChild(indicator);
                }
                updateProgressIndicators();
            }
            
            // تحديث دوائر التقدم
            function updateProgressIndicators() {
                for (let i = 1; i <= totalQuestions; i++) {
                    const indicator = document.getElementById(`indicator${i}`);
                    indicator.classList.remove('current', 'correct', 'incorrect');
                    
                    if (i === currentQuestion) {
                        indicator.classList.add('current');
                    } else if (userAnswers[i]) {
                        if (userAnswers[i].isCorrect) {
                            indicator.classList.add('correct');
                        } else {
                            indicator.classList.add('incorrect');
                        }
                    }
                }
            }
            
            // بدء الاختبار
            startBtn.addEventListener('click', function() {
                const studentName = studentNameInput.value.trim();
                const section = sectionSelect.value;
                
                if (!studentName || !section) {
                    alert('يرجى إدخال الاسم واختيار الشعبة');
                    return;
                }
                
                studentInfo.style.display = 'none';
                progressIndicators.style.display = 'flex';
                quizContainer.style.display = 'block';
                
                createProgressIndicators();
                showQuestion(currentQuestion);
            });
            
            // عرض السؤال
            function showQuestion(questionNumber) {
                // إخفاء جميع الأسئلة
                document.querySelectorAll('.question').forEach(q => {
                    q.classList.remove('active');
                });
                
                // عرض السؤال الحالي
                const currentQuestionElement = document.getElementById(`question${questionNumber}`);
                if (currentQuestionElement) {
                    currentQuestionElement.classList.add('active');
                }
                
                updateProgressIndicators();
            }
            
            // معالجة اختيار الإجابة
            document.addEventListener('click', function(e) {
                if (e.target.classList.contains('option') && 
                    !e.target.classList.contains('correct') && 
                    !e.target.classList.contains('incorrect')) {
                    
                    const questionElement = e.target.closest('.question');
                    const questionId = questionElement.id.replace('question', '');
                    const options = questionElement.querySelectorAll('.option');
                    const nextBtn = document.getElementById(`nextBtn${questionId}`);
                    const explanation = questionElement.querySelector('.explanation');
                    
                    // التحقق من الإجابة الصحيحة
                    const isCorrect = e.target.hasAttribute('data-correct');
                    
                    // تسجيل الإجابة
                    userAnswers[questionId] = {
                        answer: e.target.textContent,
                        isCorrect: isCorrect
                    };
                    
                    // تحديث النتيجة
                    if (isCorrect) {
                        score++;
                    }
                    
                    // تحديث مظهر الخيارات
                    options.forEach(option => {
                        option.classList.remove('correct', 'incorrect');
                        if (option.hasAttribute('data-correct')) {
                            option.classList.add('correct');
                        } else if (option === e.target && !isCorrect) {
                            option.classList.add('incorrect');
                        }
                    });
                    
                    // عرض التفسير
                    explanation.textContent = isCorrect ? 
                        'إجابة صحيحة! أحسنت.' : 
                        'إجابة خاطئة. الخيار الصحيح هو: ' + Array.from(options).find(o => o.hasAttribute('data-correct')).textContent;
                    explanation.className = `explanation ${isCorrect ? 'correct' : 'incorrect'}`;
                    
                    // تمكين زر التالي
                    nextBtn.disabled = false;
                    
                    // تحديث دوائر التقدم
                    updateProgressIndicators();
                    
                    // زيادة عدد الأسئلة المجابة
                    answeredQuestions++;
                    
                    // إذا كان هذا هو السؤال الأخير، عرض النتائج
                    if (parseInt(questionId) === totalQuestions) {
                        nextBtn.textContent = 'إنهاء الاختبار';
                        nextBtn.addEventListener('click', showResults);
                    } else {
                        nextBtn.addEventListener('click', function() {
                            currentQuestion++;
                            showQuestion(currentQuestion);
                        });
                    }
                }
            });
            
            // عرض النتائج
            function showResults() {
                quizContainer.style.display = 'none';
                progressIndicators.style.display = 'none';
                results.classList.add('active');
                
                // حساب النسبة المئوية
                const percentage = Math.round((score / totalQuestions) * 100);
                
                // عرض معلومات الطالب
                resultName.textContent = studentNameInput.value;
                resultSection.textContent = `الشعبة ${sectionSelect.value}`;
                
                // عرض النتيجة
                finalPercentage.textContent = `${percentage}%`;
                gradeCircle.textContent = `${percentage}%`;
                
                // تحديد التقدير
                let gradeText = '';
                if (percentage >= 90) {
                    gradeText = 'ممتاز';
                    gradeCircle.style.background = '#28a745';
                } else if (percentage >= 80) {
                    gradeText = 'جيد جداً';
                    gradeCircle.style.background = '#20c997';
                } else if (percentage >= 70) {
                    gradeText = 'جيد';
                    gradeCircle.style.background = '#17a2b8';
                } else if (percentage >= 60) {
                    gradeText = 'مقبول';
                    gradeCircle.style.background = '#ffc107';
                } else {
                    gradeText = 'راسب';
                    gradeCircle.style.background = '#dc3545';
                }
                
                finalGrade.textContent = `تقدير: ${gradeText}`;
                
                // بدء العد التنازلي لإعادة التحميل
                let countdownValue = 10;
                countdownElement.textContent = countdownValue;
                
                countdown = setInterval(function() {
                    countdownValue--;
                    countdownElement.textContent = countdownValue;
                    
                    if (countdownValue <= 0) {
                        clearInterval(countdown);
                        location.reload();
                    }
                }, 1000);
            }
        });
    </script>
</body>
</html>
