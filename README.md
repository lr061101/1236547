<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>COPD患病可能性评估</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#165DFF',
                        secondary: '#FF7D00',
                        danger: '#F53F3F',
                        warning: '#FF7D00',
                        success: '#00B42A',
                        info: '#86909C',
                        light: '#F2F3F5',
                        dark: '#1D2129',
                    },
                    fontFamily: {
                        inter: ['Inter', 'system-ui', 'sans-serif'],
                    },
                }
            }
        }
    </script>
    <style type="text/tailwindcss">
        @layer utilities {
            .content-auto {
                content-visibility: auto;
            }
            .bg-gradient-primary {
                background: linear-gradient(135deg, #165DFF 0%, #0040C9 100%);
            }
            .card-shadow {
                box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
            }
            .text-shadow {
                text-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            }
            .input-focus {
                @apply focus:ring-2 focus:ring-primary/50 focus:border-primary;
            }
        }
    </style>
</head>
<body class="font-inter bg-gray-50 text-dark min-h-screen flex flex-col">
    <!-- 导航栏 -->
    <nav class="bg-white shadow-md fixed w-full z-50 transition-all duration-300" id="navbar">
        <div class="container mx-auto px-4 py-3 flex justify-between items-center">
            <div class="flex items-center space-x-2">
                <i class="fa fa-heartbeat text-primary text-2xl"></i>
                <span class="text-xl font-bold text-dark">呼吸健康评估</span>
            </div>
            <div class="hidden md:flex items-center space-x-6">
                <a href="#assessment" class="text-gray-700 hover:text-primary transition-colors">评估工具</a>
                <a href="#about" class="text-gray-700 hover:text-primary transition-colors">关于COPD</a>
                <a href="#prevention" class="text-gray-700 hover:text-primary transition-colors">预防措施</a>
                <button class="bg-primary hover:bg-primary/90 text-white px-4 py-2 rounded-lg transition-all transform hover:scale-105 shadow-md">
                    开始评估
                </button>
            </div>
            <button class="md:hidden text-gray-700" id="menuToggle">
                <i class="fa fa-bars text-xl"></i>
            </button>
        </div>
        <!-- 移动端菜单 -->
        <div class="md:hidden hidden bg-white w-full absolute top-full left-0 shadow-lg" id="mobileMenu">
            <div class="container mx-auto px-4 py-3 flex flex-col space-y-3">
                <a href="#assessment" class="text-gray-700 hover:text-primary py-2 transition-colors">评估工具</a>
                <a href="#about" class="text-gray-700 hover:text-primary py-2 transition-colors">关于COPD</a>
                <a href="#prevention" class="text-gray-700 hover:text-primary py-2 transition-colors">预防措施</a>
                <button class="bg-primary hover:bg-primary/90 text-white px-4 py-2 rounded-lg transition-all transform hover:scale-105 shadow-md">
                    开始评估
                </button>
            </div>
        </div>
    </nav>

    <!-- 英雄区域 -->
    <header class="pt-24 pb-16 bg-gradient-primary text-white relative overflow-hidden">
        <div class="absolute inset-0 bg-[url('https://picsum.photos/id/237/1920/1080')] opacity-10 bg-cover bg-center"></div>
        <div class="container mx-auto px-4 relative z-10">
            <div class="max-w-3xl">
                <h1 class="text-[clamp(2.5rem,5vw,4rem)] font-bold leading-tight text-shadow mb-6">
                    COPD患病可能性评估
                </h1>
                <p class="text-[clamp(1rem,2vw,1.25rem)] mb-8 text-white/90 max-w-2xl">
                    通过简单的问卷，评估您患慢性阻塞性肺疾病(COPD)的风险。及早发现，采取措施，保护您的呼吸健康。
                </p>
                <div class="flex flex-col sm:flex-row gap-4">
                    <a href="#assessment" class="bg-white text-primary font-medium px-6 py-3 rounded-lg shadow-lg hover:shadow-xl transition-all transform hover:scale-105 text-center">
                        开始评估 <i class="fa fa-arrow-right ml-2"></i>
                    </a>
                    <a href="#about" class="bg-transparent border-2 border-white text-white font-medium px-6 py-3 rounded-lg hover:bg-white/10 transition-all text-center">
                        了解更多
                    </a>
                </div>
            </div>
        </div>
        <div class="absolute bottom-0 left-0 w-full h-16 bg-gradient-to-t from-gray-50 to-transparent"></div>
    </header>

    <!-- 评估表单区域 -->
    <section id="assessment" class="py-16 bg-gray-50">
        <div class="container mx-auto px-4">
            <div class="text-center mb-12">
                <h2 class="text-[clamp(1.75rem,3vw,2.5rem)] font-bold text-dark mb-4">COPD风险评估</h2>
                <p class="text-gray-600 max-w-2xl mx-auto">请根据您的实际情况回答以下问题，完成后我们将为您提供患COPD的风险评估和相关建议。</p>
            </div>

            <div class="max-w-3xl mx-auto bg-white rounded-2xl card-shadow p-6 md:p-8">
                <form id="copdAssessmentForm" class="space-y-8">
                    <!-- 个人信息 -->
                    <div class="bg-light rounded-xl p-6">
                        <h3 class="text-xl font-semibold mb-4 flex items-center">
                            <span class="bg-primary text-white w-8 h-8 rounded-full flex items-center justify-center mr-3">1</span>
                            个人信息
                        </h3>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div>
                                <label for="age" class="block text-gray-700 mb-2 font-medium">年龄</label>
                                <input type="number" id="age" min="1" max="120" class="w-full px-4 py-2 border border-gray-300 rounded-lg input-focus transition-all" placeholder="请输入您的年龄">
                            </div>
                            <div>
                                <label for="gender" class="block text-gray-700 mb-2 font-medium">性别</label>
                                <select id="gender" class="w-full px-4 py-2 border border-gray-300 rounded-lg input-focus transition-all">
                                    <option value="">请选择</option>
                                    <option value="male">男</option>
                                    <option value="female">女</option>
                                    <option value="other">其他</option>
                                </select>
                            </div>
                        </div>
                    </div>

                    <!-- 症状相关问题 -->
                    <div class="bg-light rounded-xl p-6">
                        <h3 class="text-xl font-semibold mb-6 flex items-center">
                            <span class="bg-primary text-white w-8 h-8 rounded-full flex items-center justify-center mr-3">2</span>
                            症状相关问题
                        </h3>
                        
                        <div class="space-y-6">
                            <div>
                                <label class="block text-gray-700 mb-3 font-medium">您是否有持续3个月以上的慢性咳嗽？</label>
                                <div class="flex space-x-4">
                                    <label class="inline-flex items-center">
                                        <input type="radio" name="cough" value="yes" class="form-radio h-5 w-5 text-primary">
                                        <span class="ml-2">是</span>
                                    </label>
                                    <label class="inline-flex items-center">
                                        <input type="radio" name="cough" value="no" class="form-radio h-5 w-5 text-primary">
                                        <span class="ml-2">否</span>
                                    </label>
                                </div>
                            </div>
                            
                            <div>
                                <label class="block text-gray-700 mb-3 font-medium">您是否经常咳出痰液？</label>
                                <div class="flex space-x-4">
                                    <label class="inline-flex items-center">
                                        <input type="radio" name="phlegm" value="yes" class="form-radio h-5 w-5 text-primary">
                                        <span class="ml-2">是</span>
                                    </label>
                                    <label class="inline-flex items-center">
                                        <input type="radio" name="phlegm" value="no" class="form-radio h-5 w-5 text-primary">
                                        <span class="ml-2">否</span>
                                    </label>
                                </div>
                            </div>
                            
                            <div>
                                <label class="block text-gray-700 mb-3 font-medium">您在进行体力活动时是否感到呼吸困难？</label>
                                <div class="flex space-x-4">
                                    <label class="inline-flex items-center">
                                        <input type="radio" name="breathlessness" value="yes" class="form-radio h-5 w-5 text-primary">
                                        <span class="ml-2">是</span>
                                    </label>
                                    <label class="inline-flex items-center">
                                        <input type="radio" name="breathlessness" value="no" class="form-radio h-5 w-5 text-primary">
                                        <span class="ml-2">否</span>
                                    </label>
                                </div>
                                
                                <div id="severityGroup" class="mt-4 ml-8 hidden">
                                    <label class="block text-gray-700 mb-2">如果是，呼吸困难的程度如何？</label>
                                    <div class="flex space-x-4">
                                        <label class="inline-flex items-center">
                                            <input type="radio" name="severity" value="mild" class="form-radio h-5 w-5 text-primary">
                                            <span class="ml-2">轻度</span>
                                        </label>
                                        <label class="inline-flex items-center">
                                            <input type="radio" name="severity" value="moderate" class="form-radio h-5 w-5 text-primary">
                                            <span class="ml-2">中度</span>
                                        </label>
                                        <label class="inline-flex items-center">
                                            <input type="radio" name="severity" value="severe" class="form-radio h-5 w-5 text-primary">
                                            <span class="ml-2">重度</span>
                                        </label>
                                    </div>
                                </div>
                            </div>
                            
                            <div>
                                <label class="block text-gray-700 mb-3 font-medium">您是否经常感到喘息？</label>
                                <div class="flex space-x-4">
                                    <label class="inline-flex items-center">
                                        <input type="radio" name="wheezing" value="yes" class="form-radio h-5 w-5 text-primary">
                                        <span class="ml-2">是</span>
                                    </label>
                                    <label class="inline-flex items-center">
                                        <input type="radio" name="wheezing" value="no" class="form-radio h-5 w-5 text-primary">
                                        <span class="ml-2">否</span>
                                    </label>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- 风险因素相关问题 -->
                    <div class="bg-light rounded-xl p-6">
                        <h3 class="text-xl font-semibold mb-6 flex items-center">
                            <span class="bg-primary text-white w-8 h-8 rounded-full flex items-center justify-center mr-3">3</span>
                            风险因素相关问题
                        </h3>
                        
                        <div class="space-y-6">
                            <div>
                                <label class="block text-gray-700 mb-3 font-medium">您是否有吸烟史？</label>
                                <div class="flex space-x-4">
                                    <label class="inline-flex items-center">
                                        <input type="radio" name="smoking" value="never" class="form-radio h-5 w-5 text-primary">
                                        <span class="ml-2">从未吸烟</span>
                                    </label>
                                    <label class="inline-flex items-center">
                                        <input type="radio" name="smoking" value="ex" class="form-radio h-5 w-5 text-primary">
                                        <span class="ml-2">已戒烟</span>
                                    </label>
                                    <label class="inline-flex items-center">
                                        <input type="radio" name="smoking" value="current" class="form-radio h-5 w-5 text-primary">
                                        <span class="ml-2">当前吸烟者</span>
                                    </label>
                                </div>
                                
                                <div id="smokingYearsGroup" class="mt-4 ml-8 hidden">
                                    <label for="smokingYears" class="block text-gray-700 mb-2">您吸烟多少年？</label>
                                    <input type="number" id="smokingYears" min="0" max="100" class="w-full px-4 py-2 border border-gray-300 rounded-lg input-focus transition-all" placeholder="请输入吸烟年数">
                                </div>
                                
                                <div id="packsPerDayGroup" class="mt-4 ml-8 hidden">
                                    <label for="packsPerDay" class="block text-gray-700 mb-2">您平均每天吸多少包烟？</label>
                                    <input type="number" id="packsPerDay" min="0" step="0.1" max="10" class="w-full px-4 py-2 border border-gray-300 rounded-lg input-focus transition-all" placeholder="例如：0.5">
                                </div>
                            </div>
                            
                            <div>
                                <label class="block text-gray-700 mb-3 font-medium">您的工作是否长期接触粉尘、化学物质或烟雾？</label>
                                <div class="flex space-x-4">
                                    <label class="inline-flex items-center">
                                        <input type="radio" name="occupation" value="yes" class="form-radio h-5 w-5 text-primary">
                                        <span class="ml-2">是</span>
                                    </label>
                                    <label class="inline-flex items-center">
                                        <input type="radio" name="occupation" value="no" class="form-radio h-5 w-5 text-primary">
                                        <span class="ml-2">否</span>
                                    </label>
                                </div>
                            </div>
                            
                            <div>
                                <label class="block text-gray-700 mb-3 font-medium">您是否长期生活在空气污染严重的地区？</label>
                                <div class="flex space-x-4">
                                    <label class="inline-flex items-center">
                                        <input type="radio" name="pollution" value="yes" class="form-radio h-5 w-5 text-primary">
                                        <span class="ml-2">是</span>
                                    </label>
                                    <label class="inline-flex items-center">
                                        <input type="radio" name="pollution" value="no" class="form-radio h-5 w-5 text-primary">
                                        <span class="ml-2">否</span>
                                    </label>
                                </div>
                            </div>
                            
                            <div>
                                <label class="block text-gray-700 mb-3 font-medium">您的直系亲属中是否有COPD患者？</label>
                                <div class="flex space-x-4">
                                    <label class="inline-flex items-center">
                                        <input type="radio" name="familyHistory" value="yes" class="form-radio h-5 w-5 text-primary">
                                        <span class="ml-2">是</span>
                                    </label>
                                    <label class="inline-flex items-center">
                                        <input type="radio" name="familyHistory" value="no" class="form-radio h-5 w-5 text-primary">
                                        <span class="ml-2">否</span>
                                    </label>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="text-center">
                        <button type="submit" id="submitBtn" class="bg-primary hover:bg-primary/90 text-white font-medium px-8 py-3 rounded-lg shadow-lg transition-all transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-primary/50">
                            <i class="fa fa-check-circle mr-2"></i> 提交评估
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </section>

    <!-- 结果展示区域 -->
    <section id="results" class="py-16 bg-white hidden">
        <div class="container mx-auto px-4">
            <div class="text-center mb-12">
                <h2 class="text-[clamp(1.75rem,3vw,2.5rem)] font-bold text-dark mb-4">评估结果</h2>
                <p class="text-gray-600 max-w-2xl mx-auto">根据您提供的信息，以下是您患COPD的风险评估结果。请记住，这只是初步评估，不能替代专业医疗建议。</p>
            </div>

            <div class="max-w-4xl mx-auto">
                <div class="bg-light rounded-2xl p-8 card-shadow">
                    <div class="flex flex-col md:flex-row gap-8">
                        <div class="md:w-1/3">
                            <div class="bg-white rounded-xl p-6 shadow-md text-center h-full flex flex-col justify-center">
                                <div id="riskLevelBadge" class="mb-4 w-24 h-24 mx-auto rounded-full flex items-center justify-center bg-success text-white text-2xl font-bold">
                                    低风险
                                </div>
                                <h3 class="text-xl font-bold mb-2">您的风险等级</h3>
                                <p class="text-gray-600">基于您的回答计算得出</p>
                            </div>
                        </div>
                        
                        <div class="md:w-2/3">
                            <div class="bg-white rounded-xl p-6 shadow-md mb-6">
                                <h3 class="text-xl font-bold mb-4 flex items-center">
                                    <i class="fa fa-bar-chart text-primary mr-2"></i> 评分详情
                                </h3>
                                <div class="space-y-4">
                                    <div>
                                        <div class="flex justify-between mb-1">
                                            <span class="font-medium">症状评分</span>
                                            <span id="symptomsScore" class="text-primary font-bold">0/20</span>
                                        </div>
                                        <div class="w-full bg-gray-200 rounded-full h-2.5">
                                            <div id="symptomsProgress" class="bg-primary h-2.5 rounded-full" style="width: 0%"></div>
                                        </div>
                                    </div>
                                    
                                    <div>
                                        <div class="flex justify-between mb-1">
                                            <span class="font-medium">风险因素评分</span>
                                            <span id="riskFactorsScore" class="text-secondary font-bold">0/20</span>
                                        </div>
                                        <div class="w-full bg-gray-200 rounded-full h-2.5">
                                            <div id="riskFactorsProgress" class="bg-secondary h-2.5 rounded-full" style="width: 0%"></div>
                                        </div>
                                    </div>
                                    
                                    <div>
                                        <div class="flex justify-between mb-1">
                                            <span class="font-medium">总评分</span>
                                            <span id="totalScore" class="text-dark font-bold">0/40</span>
                                        </div>
                                        <div class="w-full bg-gray-200 rounded-full h-2.5">
                                            <div id="totalProgress" class="bg-gradient-to-r from-green-400 via-yellow-500 to-red-500 h-2.5 rounded-full" style="width: 0%"></div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <div class="bg-white rounded-xl p-6 shadow-md">
                                <h3 class="text-xl font-bold mb-4 flex items-center">
                                    <i class="fa fa-info-circle text-primary mr-2"></i> 评估建议
                                </h3>
                                <p id="assessmentAdvice" class="text-gray-700 leading-relaxed">
                                    您目前患COPD的风险较低。建议保持健康的生活方式，避免吸烟和空气污染。
                                </p>
                                <div class="mt-4 text-sm text-gray-500">
                                    <i class="fa fa-exclamation-triangle mr-1"></i> 注意: 本评估仅供参考，不能替代专业医疗建议。如有疑虑，请咨询医疗专业人士。
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="mt-10 text-center">
                    <button id="newAssessmentBtn" class="bg-primary hover:bg-primary/90 text-white font-medium px-6 py-3 rounded-lg shadow-lg transition-all transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-primary/50">
                        <i class="fa fa-refresh mr-2"></i> 重新评估
                    </button>
                </div>
            </div>
        </div>
    </section>

    <!-- 关于COPD区域 -->
    <section id="about" class="py-16 bg-gray-50">
        <div class="container mx-auto px-4">
            <div class="text-center mb-12">
                <h2 class="text-[clamp(1.75rem,3vw,2.5rem)] font-bold text-dark mb-4">关于COPD</h2>
                <p class="text-gray-600 max-w-2xl mx-auto">了解慢性阻塞性肺疾病(COPD)的基本知识，包括症状、风险因素和治疗方法。</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <div class="bg-white rounded-xl p-6 card-shadow hover:shadow-lg transition-all transform hover:-translate-y-1">
                    <div class="w-16 h-16 bg-primary/10 rounded-full flex items-center justify-center mb-6 mx-auto">
                        <i class="fa fa-stethoscope text-primary text-2xl"></i>
                    </div>
                    <h3 class="text-xl font-bold mb-3 text-center">什么是COPD？</h3>
                    <p class="text-gray-600">
                        慢性阻塞性肺疾病(COPD)是一种常见的、可预防和治疗的疾病，其特征是持续的呼吸道症状和气流受限，通常是由于显著暴露于有害颗粒或气体引起的气道和/或肺泡异常所致。
                    </p>
                </div>
                
                <div class="bg-white rounded-xl p-6 card-shadow hover:shadow-lg transition-all transform hover:-translate-y-1">
                    <div class="w-16 h-16 bg-primary/10 rounded-full flex items-center justify-center mb-6 mx-auto">
                        <i class="fa fa-medkit text-primary text-2xl"></i>
                    </div>
                    <h3 class="text-xl font-bold mb-3 text-center">主要症状</h3>
                    <ul class="text-gray-600 space-y-2">
                        <li class="flex items-start">
                            <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                            <span>慢性咳嗽，可能伴有痰液</span>
                        </li>
                        <li class="flex items-start">
                            <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                            <span>进行性呼吸困难，特别是在体力活动时</span>
                        </li>
                        <li class="flex items-start">
                            <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                            <span>喘息和胸闷</span>
                        </li>
                        <li class="flex items-start">
                            <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                            <span>反复呼吸道感染</span>
                        </li>
                    </ul>
                </div>
                
                <div class="bg-white rounded-xl p-6 card-shadow hover:shadow-lg transition-all transform hover:-translate-y-1">
                    <div class="w-16 h-16 bg-primary/10 rounded-full flex items-center justify-center mb-6 mx-auto">
                        <i class="fa fa-exclamation-triangle text-primary text-2xl"></i>
                    </div>
                    <h3 class="text-xl font-bold mb-3 text-center">风险因素</h3>
                    <ul class="text-gray-600 space-y-2">
                        <li class="flex items-start">
                            <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                            <span>吸烟（包括主动和被动吸烟）</span>
                        </li>
                        <li class="flex items-start">
                            <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                            <span>长期暴露于职业粉尘和化学物质</span>
                        </li>
                        <li class="flex items-start">
                            <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                            <span>空气污染</span>
                        </li>
                        <li class="flex items-start">
                            <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                            <span>遗传因素（如α1-抗胰蛋白酶缺乏）</span>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </section>

    <!-- 预防措施区域 -->
    <section id="prevention" class="py-16 bg-white">
        <div class="container mx-auto px-4">
            <div class="text-center mb-12">
                <h2 class="text-[clamp(1.75rem,3vw,2.5rem)] font-bold text-dark mb-4">COPD预防措施</h2>
                <p class="text-gray-600 max-w-2xl mx-auto">采取以下措施可以降低患COPD的风险，保护您的呼吸健康。</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                <div class="bg-light rounded-xl p-6">
                    <h3 class="text-xl font-bold mb-4 flex items-center">
                        <i class="fa fa-smoking-ban text-danger mr-2"></i>
                        戒烟
                    </h3>
                    <p class="text-gray-600 mb-4">
                        吸烟是COPD的主要危险因素。戒烟是降低COPD风险的最重要步骤。无论吸烟多久，戒烟都能带来健康益处。
                    </p>
                    <div class="bg-white rounded-lg p-4 shadow-sm">
                        <h4 class="font-bold mb-2">戒烟小贴士：</h4>
                        <ul class="text-gray-600 space-y-2">
                            <li class="flex items-start">
                                <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                                <span>设定戒烟日期并坚持下去</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                                <span>寻求家人和朋友的支持</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                                <span>考虑使用戒烟辅助工具</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                                <span>避免触发吸烟的情境和活动</span>
                            </li>
                        </ul>
                    </div>
                </div>
                
                <div class="bg-light rounded-xl p-6">
                    <h3 class="text-xl font-bold mb-4 flex items-center">
                        <i class="fa fa-leaf text-success mr-2"></i>
                        减少暴露于污染物
                    </h3>
                    <p class="text-gray-600 mb-4">
                        避免或减少暴露于职业粉尘、化学物质和空气污染，可以显著降低患COPD的风险。
                    </p>
                    <div class="bg-white rounded-lg p-4 shadow-sm">
                        <h4 class="font-bold mb-2">减少暴露的方法：</h4>
                        <ul class="text-gray-600 space-y-2">
                            <li class="flex items-start">
                                <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                                <span>在工作场所使用防护装备</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                                <span>使用空气净化器改善室内空气质量</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                                <span>避免在高污染时段外出</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                                <span>使用清洁的烹饪燃料</span>
                            </li>
                        </ul>
                    </div>
                </div>
                
                <div class="bg-light rounded-xl p-6">
                    <h3 class="text-xl font-bold mb-4 flex items-center">
                        <i class="fa fa-heartbeat text-primary mr-2"></i>
                        保持健康生活方式
                    </h3>
                    <p class="text-gray-600 mb-4">
                        健康的生活方式有助于增强免疫系统，保持肺部健康，降低患COPD的风险。
                    </p>
                    <div class="bg-white rounded-lg p-4 shadow-sm">
                        <h4 class="font-bold mb-2">健康生活方式建议：</h4>
                        <ul class="text-gray-600 space-y-2">
                            <li class="flex items-start">
                                <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                                <span>均衡饮食，多吃水果、蔬菜和全谷物</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                                <span>定期进行适度的体育锻炼</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                                <span>保持健康体重</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                                <span>充足睡眠，保持良好的作息习惯</span>
                            </li>
                        </ul>
                    </div>
                </div>
                
                <div class="bg-light rounded-xl p-6">
                    <h3 class="text-xl font-bold mb-4 flex items-center">
                        <i class="fa fa-user-md text-info mr-2"></i>
                        定期体检和疫苗接种
                    </h3>
                    <p class="text-gray-600 mb-4">
                        定期体检可以早期发现COPD和其他健康问题，及时采取干预措施。疫苗接种可以预防呼吸道感染，降低COPD恶化的风险。
                    </p>
                    <div class="bg-white rounded-lg p-4 shadow-sm">
                        <h4 class="font-bold mb-2">建议的疫苗和体检：</h4>
                        <ul class="text-gray-600 space-y-2">
                            <li class="flex items-start">
                                <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                                <span>每年接种流感疫苗</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                                <span>接种肺炎球菌疫苗</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                                <span>定期进行肺功能检查</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa fa-check-circle text-primary mt-1 mr-2"></i>
                                <span>遵循医生的健康检查建议</span>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- 页脚 -->
    <footer class="bg-dark text-white py-12">
        <div class="container mx-auto px-4">
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <div>
