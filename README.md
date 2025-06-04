class Question:
    """表示一个评估问题"""
    def __init__(self, text, options, weight=1):
        self.text = text
        self.options = options  # 字典：选项文本 -> (分数, 后续问题索引列表)
        self.weight = weight    # 问题权重

class DiseaseModel:
    """表示一种疾病的评估模型"""
    def __init__(self, name, description, questions, risk_levels):
        self.name = name
        self.description = description
        self.questions = questions
        self.risk_levels = risk_levels  # 风险级别列表：[(分数下限, 分数上限, 描述, 建议)]
    
    def calculate_score(self, answers):
        """根据用户回答计算总分"""
        total_score = 0
        for i, answer in enumerate(answers):
            if i < len(self.questions):
                question = self.questions[i]
                if answer in question.options:
                    score, _ = question.options[answer]
                    total_score += score * question.weight
        return total_score
    
    def get_risk_level(self, score):
        """根据总分获取风险级别"""
        for min_score, max_score, description, advice in self.risk_levels:
            if min_score <= score <= max_score:
                return description, advice
        return "无法评估", "建议咨询专业医生"

class RiskAssessmentSystem:
    """风险评估系统"""
    def __init__(self):
        self.models = {}
    
    def add_model(self, model):
        """添加疾病评估模型"""
        self.models[model.name] = model
    
    def assess_disease(self, disease_name):
        """评估特定疾病的风险"""
        if disease_name not in self.models:
            print(f"错误：未找到疾病模型 '{disease_name}'")
            return
        
        model = self.models[disease_name]
        print(f"\n=== {model.name} 风险评估 ===")
        print(model.description)
        print("-" * 50)
        
        answers = []
        current_questions = [0]  # 从第一个问题开始
        
        while current_questions:
            next_questions = []
            for q_idx in current_questions:
                if q_idx < len(model.questions):
                    question = model.questions[q_idx]
                    print(f"\n{len(answers) + 1}. {question.text}")
                    
                    # 显示选项
                    options_list = list(question.options.keys())
                    for i, option in enumerate(options_list):
                        print(f"   {i+1}. {option}")
                    
                    # 获取用户回答
                    valid_input = False
                    while not valid_input:
                        answer_idx = input(f"请选择选项 (1-{len(options_list)}): ")
                        try:
                            answer_idx = int(answer_idx) - 1
                            if 0 <= answer_idx < len(options_list):
                                selected_option = options_list[answer_idx]
                                answers.append(selected_option)
                                # 获取后续问题
                                _, follow_up = question.options[selected_option]
                                next_questions.extend(follow_up)
                                valid_input = True
                            else:
                                print("输入无效，请重新选择")
                        except ValueError:
                            print("输入无效，请输入数字")
            current_questions = next_questions
        
        # 计算分数并显示结果
        score = model.calculate_score(answers)
        description, advice = model.get_risk_level(score)
        
        print("-" * 50)
        print(f"您的{model.name}风险评估总分为: {score}分")
        print(f"风险等级: {description}")
        print(f"建议: {advice}")
        print("\n注意：本评估仅供参考，不能替代专业医疗诊断。")

def create_copd_model():
    """创建COPD评估模型"""
    questions = [
        Question(
            "您的年龄是多少？",
            {
                "小于40岁": (0, []),
                "40-50岁": (1, []),
                "51-60岁": (2, []),
                "61-70岁": (3, []),
                "大于70岁": (4, [])
            },
            weight=1.5
        ),
        Question(
            "您的吸烟状况如何？",
            {
                "从不吸烟": (0, [2]),
                "曾经吸烟但已戒烟": (2, [3]),
                "当前吸烟者": (4, [3])
            },
            weight=2
        ),
        Question(
            "您是否长期暴露于粉尘、化学物质或空气污染环境中？",
            {
                "否": (0, []),
                "是，偶尔": (1, []),
                "是，经常": (3, [])
            },
            weight=1.5
        ),
        Question(
            "您的吸烟量是多少包年？(例如: 每天1包，吸了20年为20包年)",
            {
                "小于10包年": (1, []),
                "10-20包年": (2, []),
                "21-30包年": (3, []),
                "大于30包年": (4, [])
            },
            weight=2
        ),
        Question(
            "您是否有呼吸困难的症状？",
            {
                "无": (0, []),
                "仅在剧烈活动时": (1, []),
                "在平地行走时": (2, []),
                "穿衣或脱衣时": (3, [])
            },
            weight=2
        ),
        Question(
            "您是否有慢性咳嗽？",
            {
                "否": (0, []),
                "是，偶尔": (1, [6]),
                "是，经常": (2, [6])
            },
            weight=1.5
        ),
        Question(
            "咳嗽是否伴有咳痰？",
            {
                "否": (0, []),
                "是，偶尔": (1, []),
                "是，经常": (2, [])
            },
            weight=1.5
        ),
        Question(
            "您是否有喘息或胸闷的症状？",
            {
                "否": (0, []),
                "是，偶尔": (1, []),
                "是，经常": (2, []),
                "是，持续存在": (3, [])
            },
            weight=1.5
        ),
        Question(
            "您的直系亲属中是否有COPD患者？",
            {
                "否": (0, []),
                "是": (2, [])
            },
            weight=1.5
        ),
        Question(
            "您每年是否有多次呼吸道感染？",
            {
                "否": (0, []),
                "是": (1, [10])
            },
            weight=1
        ),
        Question(
            "每年大约几次？",
            {
                "1-2次": (1, []),
                "3-4次": (2, []),
                "5次或更多": (3, [])
            },
            weight=1
        )
    ]
    
    risk_levels = [
        (0, 5, "低风险", "您目前的症状和风险因素提示COPD的可能性较低。建议保持健康的生活方式，避免吸烟和空气污染。"),
        (6, 12, "中度风险", "您有一些COPD的风险因素和症状。建议咨询医生进行肺功能测试，如FEV1/FVC比值检测。"),
        (13, 18, "高度风险", "您的症状和风险因素高度提示COPD的可能性。建议立即咨询呼吸科医生，进行全面的肺功能评估和胸部影像学检查。"),
        (19, 100, "极高风险", "您的症状和风险因素非常符合COPD，需要紧急医疗评估。建议尽快就医，可能需要进行胸部CT、血气分析等进一步检查。")
    ]
    
    return DiseaseModel(
        "慢性阻塞性肺疾病(COPD)",
        "本评估工具将根据您的症状和风险因素评估您患COPD的可能性。",
        questions,
        risk_levels
    )

def create_asthma_model():
    """创建哮喘评估模型"""
    questions = [
        Question(
            "您是否有反复发作的喘息？",
            {
                "否": (0, []),
                "是，偶尔": (1, [1]),
                "是，经常": (3, [1])
            },
            weight=2
        ),
        Question(
            "喘息通常在什么情况下出现？",
            {
                "运动后": (1, []),
                "接触过敏原后": (2, []),
                "夜间或清晨": (2, []),
                "以上皆是": (3, [])
            },
            weight=1.5
        ),
        Question(
            "您是否有反复发作的咳嗽？",
            {
                "否": (0, []),
                "是，主要在夜间": (2, []),
                "是，运动后": (1, []),
                "是，接触过敏原后": (2, [])
            },
            weight=1.5
        ),
        Question(
            "您是否有胸闷或胸部紧迫感？",
            {
                "否": (0, []),
                "是，偶尔": (1, []),
                "是，经常": (2, [])
            },
            weight=1.5
        ),
        Question(
            "您的症状是否在接触以下物质后加重？（可多选）",
            {
                "花粉、尘螨或宠物皮屑": (2, []),
                "烟雾、香水或化学气味": (2, []),
                "冷空气": (1, []),
                "运动": (1, []),
                "以上都没有": (0, [])
            },
            weight=1.5
        ),
        Question(
            "您或您的直系亲属是否有过敏史？",
            {
                "否": (0, []),
                "是，过敏性鼻炎": (1, []),
                "是，湿疹": (1, []),
                "是，食物或药物过敏": (1, []),
                "是，多种过敏": (2, [])
            },
            weight=1.5
        ),
        Question(
            "您的症状多久发作一次？",
            {
                "少于每周1次": (1, []),
                "每周1-2次": (2, []),
                "每天": (3, []),
                "持续存在": (4, [])
            },
            weight=2
        ),
        Question(
            "您是否使用过哮喘药物（如沙丁胺醇）缓解症状？",
            {
                "否": (0, []),
                "是，偶尔使用": (2, []),
                "是，经常使用": (3, [])
            },
            weight=2
        )
    ]
    
    risk_levels = [
        (0, 5, "低风险", "您目前的症状和风险因素提示哮喘的可能性较低。建议继续观察症状变化。"),
        (6, 12, "中度风险", "您有一些哮喘的典型症状。建议咨询医生进行肺功能测试和过敏原检测。"),
        (13, 20, "高度风险", "您的症状高度提示哮喘的可能性。建议立即咨询呼吸科医生，进行支气管激发试验等确诊检查。"),
        (21, 100, "极高风险", "您的症状非常符合哮喘，需要紧急医疗评估。建议尽快就医并开始适当的治疗。")
    ]
    
    return DiseaseModel(
        "哮喘",
        "本评估工具将根据您的症状和风险因素评估您患哮喘的可能性。",
        questions,
        risk_levels
    )

def main():
    """主函数"""
    # 创建风险评估系统
    system = RiskAssessmentSystem()
    
    # 添加疾病模型
    system.add_model(create_copd_model())
    system.add_model(create_asthma_model())
    
    print("欢迎使用疾病风险评估系统")
    print("本系统可以评估多种疾病的患病可能性")
    print("-" * 50)
    
    while True:
        print("\n可用的评估模型:")
        for i, name in enumerate(system.models.keys(), 1):
            print(f"{i}. {name}")
        
        print("0. 退出系统")
        
        choice = input("请选择要评估的疾病 (输入编号): ")
        
        if choice == "0":
            print("感谢使用疾病风险评估系统，再见！")
            break
        
        try:
            choice_idx = int(choice) - 1
            disease_names = list(system.models.keys())
            if 0 <= choice_idx < len(disease_names):
                selected_disease = disease_names[choice_idx]
                system.assess_disease(selected_disease)
            else:
                print("无效的选择，请重试")
        except ValueError:
            print("无效的输入，请输入数字")

if __name__ == "__main__":
    main()

