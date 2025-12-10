# ---A-S-
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>가전제품 A/S 센터 찾기</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            color: white;
            margin-bottom: 40px;
            padding: 20px;
        }

        h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .subtitle {
            font-size: 1.1em;
            opacity: 0.9;
        }

        .search-section {
            background: white;
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            margin-bottom: 30px;
        }

        .filter-group {
            margin-bottom: 30px;
        }

        label {
            display: block;
            font-size: 1.1em;
            font-weight: 600;
            color: #333;
            margin-bottom: 10px;
        }

        select, input {
            width: 100%;
            padding: 15px;
            font-size: 1em;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            background: white;
            transition: all 0.3s;
        }

        select:focus, input:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .search-btn {
            width: 100%;
            padding: 18px;
            font-size: 1.2em;
            font-weight: 600;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .search-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(102, 126, 234, 0.4);
        }

        .search-btn:active {
            transform: translateY(0);
        }

        .results-section {
            background: white;
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            display: none;
        }

        .results-section.show {
            display: block;
        }

        .result-card {
            background: #f8f9fa;
            border-left: 4px solid #667eea;
            padding: 25px;
            margin-bottom: 20px;
            border-radius: 10px;
            transition: transform 0.2s;
        }

        .result-card:hover {
            transform: translateX(5px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .brand-name {
            font-size: 1.4em;
            font-weight: 700;
            color: #667eea;
            margin-bottom: 15px;
        }

        .info-row {
            display: flex;
            align-items: center;
            margin: 10px 0;
            font-size: 1em;
        }

        .info-label {
            font-weight: 600;
            color: #555;
            min-width: 100px;
        }

        .info-value {
            color: #333;
        }

        .phone-link {
            color: #667eea;
            text-decoration: none;
            font-weight: 600;
        }

        .phone-link:hover {
            text-decoration: underline;
        }

        .no-results {
            text-align: center;
            padding: 40px;
            color: #666;
            font-size: 1.1em;
        }

        @media (max-width: 768px) {
            h1 {
                font-size: 1.8em;
            }

            .search-section, .results-section {
                padding: 25px;
            }

            .result-card {
                padding: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🔧 가전제품 A/S 센터 찾기</h1>
            <p class="subtitle">제품 종류와 브랜드를 선택하여 빠르게 A/S 센터를 찾아보세요</p>
        </header>

        <div class="search-section">
            <div class="filter-group">
                <label for="category">제품 카테고리</label>
                <select id="category">
                    <option value="">선택해주세요</option>
                    <option value="refrigerator">냉장고</option>
                    <option value="washer">세탁기</option>
                    <option value="tv">TV</option>
                    <option value="aircon">에어컨</option>
                    <option value="microwave">전자레인지</option>
                    <option value="vacuum">청소기</option>
                </select>
            </div>

            <div class="filter-group">
                <label for="brand">브랜드</label>
                <select id="brand">
                    <option value="">선택해주세요</option>
                    <option value="samsung">삼성</option>
                    <option value="lg">LG</option>
                    <option value="daewoo">대우</option>
                    <option value="coway">코웨이</option>
                </select>
            </div>

            <div class="filter-group">
                <label for="region">지역</label>
                <input type="text" id="region" placeholder="예: 서울, 부산, 대구 등">
            </div>

            <button class="search-btn" onclick="searchService()">A/S 센터 찾기</button>
        </div>

        <div class="results-section" id="results">
            <h2 style="margin-bottom: 25px; color: #333;">검색 결과</h2>
            <div id="resultsContent"></div>
        </div>
    </div>

    <script>
        const serviceData = {
            samsung: {
                name: '삼성전자',
                phone: '1588-3366',
                website: 'https://www.samsung.com/sec/support/',
                hours: '평일 09:00-18:00'
            },
            lg: {
                name: 'LG전자',
                phone: '1544-7777',
                website: 'https://www.lge.co.kr/support',
                hours: '평일 09:00-18:00'
            },
            daewoo: {
                name: '대우전자',
                phone: '1588-1588',
                website: 'https://www.daewooelectronics.co.kr',
                hours: '평일 09:00-18:00'
            },
            coway: {
                name: '코웨이',
                phone: '1588-5200',
                website: 'https://www.coway.co.kr',
                hours: '평일 09:00-18:00'
            }
        };

        const categoryNames = {
            refrigerator: '냉장고',
            washer: '세탁기',
            tv: 'TV',
            aircon: '에어컨',
            microwave: '전자레인지',
            vacuum: '청소기'
        };

        function searchService() {
            const category = document.getElementById('category').value;
            const brand = document.getElementById('brand').value;
            const region = document.getElementById('region').value;

            if (!category || !brand) {
                alert('제품 카테고리와 브랜드를 선택해주세요.');
                return;
            }

            const resultsSection = document.getElementById('results');
            const resultsContent = document.getElementById('resultsContent');

            const service = serviceData[brand];
            
            let html = `
                <div class="result-card">
                    <div class="brand-name">${service.name} ${categoryNames[category]} A/S</div>
                    <div class="info-row">
                        <span class="info-label">📞 고객센터:</span>
                        <span class="info-value"><a href="tel:${service.phone}" class="phone-link">${service.phone}</a></span>
                    </div>
                    <div class="info-row">
                        <span class="info-label">🌐 웹사이트:</span>
                        <span class="info-value"><a href="${service.website}" target="_blank" class="phone-link">바로가기</a></span>
                    </div>
                    <div class="info-row">
                        <span class="info-label">⏰ 운영시간:</span>
                        <span class="info-value">${service.hours}</span>
                    </div>
                    ${region ? `<div class="info-row">
                        <span class="info-label">📍 검색지역:</span>
                        <span class="info-value">${region}</span>
                    </div>` : ''}
                    <div style="margin-top: 20px; padding-top: 20px; border-top: 1px solid #ddd; color: #666;">
                        💡 고객센터로 전화하시면 가까운 서비스 센터를 안내받으실 수 있습니다.
                    </div>
                </div>
            `;

            resultsContent.innerHTML = html;
            resultsSection.classList.add('show');
            resultsSection.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
        }
    </script>
</body>
</html>
