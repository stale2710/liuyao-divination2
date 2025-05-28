<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>六爻数字起卦系统</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Microsoft YaHei', '微软雅黑', sans-serif;
        }

        body {
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #1a2a6c);
            color: #333;
            min-height: 100vh;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            width: 100%;
            max-width: 1000px;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            overflow: hidden;
        }

        header {
            background: linear-gradient(to right, #8e2de2, #4a00e0);
            color: white;
            padding: 25px;
            text-align: center;
            position: relative;
        }

        h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }

        .subtitle {
            font-size: 1.1rem;
            opacity: 0.9;
        }

        .content {
            display: flex;
            flex-wrap: wrap;
            padding: 25px;
        }

        .input-section {
            flex: 1;
            min-width: 300px;
            padding: 20px;
            background: #f8f9fa;
            border-radius: 10px;
            margin-right: 20px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
        }

        .result-section {
            flex: 1;
            min-width: 300px;
            padding: 20px;
            background: #fff;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
        }

        h2 {
            color: #5a4ae3;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid #eaeaea;
            font-size: 1.8rem;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #555;
        }

        input, textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s;
        }

            input:focus, textarea:focus {
                border-color: #5a4ae3;
                outline: none;
                box-shadow: 0 0 0 2px rgba(90, 74, 227, 0.2);
            }

        .number-inputs {
            display: flex;
            gap: 10px;
        }

            .number-inputs input {
                text-align: center;
                flex: 1;
            }

        button {
            background: linear-gradient(to right, #5a4ae3, #8e2de2);
            color: white;
            border: none;
            padding: 14px 25px;
            font-size: 18px;
            border-radius: 8px;
            cursor: pointer;
            width: 100%;
            font-weight: bold;
            letter-spacing: 1px;
            transition: transform 0.3s, box-shadow 0.3s;
        }

            button:hover {
                transform: translateY(-3px);
                box-shadow: 0 5px 15px rgba(90, 74, 227, 0.4);
            }

        .gua-container {
            background: #f0f4f8;
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 20px;
            text-align: center;
        }

        .gua-header {
            font-size: 1.5rem;
            font-weight: bold;
            margin-bottom: 15px;
            color: #5a4ae3;
        }

        .gua-symbol {
            font-size: 3rem;
            margin: 10px 0;
            letter-spacing: 10px;
        }

        .gua-name {
            font-size: 1.8rem;
            font-weight: bold;
            color: #d32f2f;
            margin: 15px 0;
        }

        .gua-info {
            display: flex;
            justify-content: space-around;
            margin: 20px 0;
            font-size: 1.1rem;
        }

        .moving-yao {
            background: #ffeb3b;
            padding: 5px 15px;
            border-radius: 20px;
            font-weight: bold;
        }

        .explanation {
            background: #fff;
            border-left: 4px solid #5a4ae3;
            padding: 15px;
            margin-top: 20px;
            border-radius: 0 8px 8px 0;
        }

        .divination-result {
            background: #e8f5e9;
            padding: 15px;
            border-radius: 8px;
            margin-top: 20px;
        }

        .result-title {
            font-weight: bold;
            color: #2e7d32;
            margin-bottom: 10px;
            font-size: 1.2rem;
        }

        .detailed-advice {
            background: #e3f2fd;
            padding: 15px;
            border-radius: 8px;
            margin-top: 20px;
        }

        .advice-title {
            font-weight: bold;
            color: #1565c0;
            margin-bottom: 10px;
            font-size: 1.2rem;
        }

        .advice-section {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 10px;
        }

        .advice-card {
            flex: 1;
            min-width: 200px;
            background: white;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        .card-title {
            font-weight: bold;
            margin-bottom: 8px;
            color: #5a4ae3;
        }

        .history-section {
            margin-top: 30px;
            padding: 20px;
            background: #f8f9fa;
            border-radius: 10px;
        }

        .history-item {
            background: white;
            border-radius: 8px;
            padding: 15px;
            margin: 10px 0;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
            cursor: pointer;
            transition: all 0.3s;
        }

            .history-item:hover {
                transform: translateY(-3px);
                box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            }

        @media (max-width: 768px) {
            .content {
                flex-direction: column;
            }

            .input-section {
                margin-right: 0;
                margin-bottom: 20px;
            }

            .gua-info {
                flex-direction: column;
                align-items: center;
                gap: 10px;
            }

            .advice-section {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>六爻数字起卦系统</h1>
            <div class="subtitle">输入三个数字，解读天地玄机</div>
        </header>

        <div class="content">
            <div class="input-section">
                <h2>起卦信息</h2>

                <div class="form-group">
                    <label for="numbers">请输入三个数字（用空格分隔）：</label>
                    <div class="number-inputs">
                        <input type="number" id="num1" min="0" max="999" placeholder="数字1" value="3">
                        <input type="number" id="num2" min="0" max="999" placeholder="数字2" value="7">
                        <input type="number" id="num3" min="0" max="999" placeholder="数字3" value="2">
                    </div>
                </div>

                <div class="form-group">
                    <label for="query">询问事由：</label>
                    <textarea id="query" rows="3" placeholder="请输入您要询问的事情...">事业发展如何？</textarea>
                </div>

                <button id="divinateBtn">起卦解卦</button>

                <div class="explanation">
                    <h3>起卦说明：</h3>
                    <p>六爻起卦法源自《易经》，通过输入三个数字：</p>
                    <ul style="padding-left: 20px; margin-top: 10px;">
                        <li>第一个数字确定上卦（除以8取余数）</li>
                        <li>第二个数字确定下卦（除以8取余数）</li>
                        <li>第三个数字确定动爻（除以6取余数）</li>
                    </ul>
                    <p style="margin-top: 10px;">系统将根据卦象和动爻位置，结合您的事由进行详细解卦。</p>
                </div>
            </div>

            <div class="result-section">
                <h2>卦象结果</h2>

                <div class="gua-container">
                    <div class="gua-header">本卦</div>
                    <div class="gua-symbol" id="originalSymbol">☲☶</div>
                    <div class="gua-name" id="originalName">火山旅</div>

                    <div class="gua-header">变卦</div>
                    <div class="gua-symbol" id="changedSymbol">☴☲</div>
                    <div class="gua-name" id="changedName">风火家人</div>

                    <div class="gua-info">
                        <div>动爻位置：<span class="moving-yao" id="movingYao">第2爻</span></div>
                        <div>询问事由：<span id="queryResult">事业发展如何？</span></div>
                    </div>
                </div>

                <div class="divination-result">
                    <div class="result-title">卦象解析：</div>
                    <p id="divinationText">本卦为火山旅卦，象征旅行、变动或不稳定状态。变卦为风火家人卦，提示最终可能回归稳定或家庭关系。动爻在第二爻，反映当前阶段需注意人际协调或行动节奏。对于事业发展，此卦象表明您可能处于变动期，需要谨慎应对环境变化，同时重视团队合作和家庭支持，未来可回归稳定状态。</p>
                </div>

                <div class="detailed-advice">
                    <div class="advice-title">详细建议：</div>
                    <div id="detailedAdvice">
                        <div class="advice-section">
                            <div class="advice-card">
                                <div class="card-title">事业发展建议</div>
                                <p>1. 近期可能有岗位变动或出差机会，宜把握但需谨慎评估</p>
                                <p>2. 加强与团队成员的沟通协作，避免单打独斗</p>
                                <p>3. 关注行业趋势变化，提前做好应对准备</p>
                            </div>
                            <div class="advice-card">
                                <div class="card-title">人际关系建议</div>
                                <p>1. 注意与上级领导的沟通方式，保持谦逊态度</p>
                                <p>2. 避免卷入办公室政治，保持中立立场</p>
                                <p>3. 可寻求年长或有经验人士的指导</p>
                            </div>
                            <div class="advice-card">
                                <div class="card-title">时机把握建议</div>
                                <p>1. 未来3个月是关键调整期，不宜做重大决策</p>
                                <p>2. 今年秋季可能有重要发展机遇出现</p>
                                <p>3. 注意农历五月和九月的关键时间节点</p>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="history-section">
                    <h2>历史解卦记录</h2>
                    <div class="history-item">
                        <strong>2025-5-28</strong> | 数字：7, 2, 4 | 事由：学业考试
                        <div>本卦：山地剥 → 变卦：风地观</div>
                    </div>
                    <div class="history-item">
                        <strong>2025-5-27</strong> | 数字：5, 9, 3 | 事由：感情发展
                        <div>本卦：风水涣 → 变卦：天水讼</div>
                    </div>
                    <div class="history-item">
                        <strong>2025-5-25</strong> | 数字：2, 6, 1 | 事由：投资决策
                        <div>本卦：泽水困 → 变卦：泽地萃</div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // 扩展卦象数据库
        const trigrams = {
            1: { name: "乾", symbol: "☰", element: "天", nature: "刚健" },
            2: { name: "兑", symbol: "☱", element: "泽", nature: "喜悦" },
            3: { name: "离", symbol: "☲", element: "火", nature: "明丽" },
            4: { name: "震", symbol: "☳", element: "雷", nature: "震动" },
            5: { name: "巽", symbol: "☴", element: "风", nature: "顺从" },
            6: { name: "坎", symbol: "☵", element: "水", nature: "险陷" },
            7: { name: "艮", symbol: "☶", element: "山", nature: "静止" },
            0: { name: "坤", symbol: "☷", element: "地", nature: "柔顺" }
        };

        // 六十四卦数据库
        const hexagrams = {
            "离艮": {
                name: "火山旅",
                changed: "风火家人",
                meaning: "旅卦象征旅行、不安定和变动。表示处于不稳定状态，需要谨慎行事",
                interpretation: "火山旅卦，上离下艮，火在山上燃烧，象征旅途中的不安定。此卦表示你正处于一个变动期，可能在外奔波或内心不安。"
            },
            "乾坤": {
                name: "天地否",
                changed: "地天泰",
                meaning: "否卦象征闭塞不通，需要等待转机",
                interpretation: "天地否卦，上乾下坤，天地不交，万物不通。表示当前处境困难，需要耐心等待转机。"
            },
            "坎离": {
                name: "水火既济",
                changed: "火水未济",
                meaning: "既济卦象征事情已成，但需谨慎守成",
                interpretation: "水火既济卦，上坎下离，水在火上，象征烹饪完成。表示事情已经成功，但需要保持谨慎。"
            },
            "震巽": {
                name: "雷风恒",
                changed: "风雷益",
                meaning: "恒卦象征持久稳定，需要持之以恒",
                interpretation: "雷风恒卦，上震下巽，雷风相激，象征持久。表示需要保持恒心，坚持不懈。"
            },
            "艮兑": {
                name: "山泽损",
                changed: "泽山咸",
                meaning: "损卦象征减损付出，有失有得",
                interpretation: "山泽损卦，上艮下兑，山下有泽，象征减损。表示需要适当付出才能有所收获。"
            },
            "巽乾": {
                name: "风天小畜",
                changed: "风火家人",
                meaning: "小畜卦象征小有积蓄，需要积累力量",
                interpretation: "风天小畜卦，上巽下乾，风行天上，象征小有积蓄。表示需要积累力量，等待时机。"
            },
            "坤艮": {
                name: "地山谦",
                changed: "地火明夷",
                meaning: "谦卦象征谦虚谨慎，以柔克刚",
                interpretation: "地山谦卦，上坤下艮，地中有山，象征谦虚。表示应以谦逊态度行事，以柔克刚。"
            },
            "离坤": {
                name: "火地晋",
                changed:
