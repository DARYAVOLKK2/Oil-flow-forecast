# Oil-flow-forecast

Прогноз дебита нефти
Необходимо построить модель для прогноза забойного давления скважины на имеющихся данных о режиме работы скважины.
Задача представлена Центром компетенций по развитию интегрированного моделирования активов ООО «Газпромнефть НТЦ»

---------------------------------------------------------------------------------------------------------------------------------------
Подробное описание

Описание задачи:
Ваша цель – построить модель для прогнозирования забойного давления скважины, опираясь на данные о режиме работы скважины, рассчитанные на программном продукте.
Данные представлены в формате таблицы, в которой целевой переменной является забойное давление. Дебит жидкости, обводненность, газовый фактор и устьевое давление – необходимые переменные для обучения.
Дебит жидкости (LIQ) – объем ежедневно добываемой из скважины жидкости. Является ключевой характеристикой ее работы, определяющей способность скважины генерировать продукт при заданном режиме эксплуатации.
Обводненность (WCT) – содержание воды в добываемой продукции со скважины, определяемое как отношение дебита нефти к дебиту жидкости.
WCT = Qводы / (Qнефти + Qводы) 
Газовый фактор (GOR) – отношение объема добытого газа к объёму добытой нефти в поверхностных условиях.
GOR = Qгаза / Qнефти
Устьевое давление (THP) – давление на устье скважины (на поверхности).
Забойное давление (BHP) – давление на забое скважины (в пласте).
Выборка, представленная в виде таблицы, характеризует работу скважины. По данной таблице возможно определить зависимость забойного давления скважины от его дебита жидкости при конкретных условиях. Данную зависимость называют кривой оттока (Vertical Flow Performance).
Корректный вид кривой представлен на рисунке 1.

Рисунок 1 – Кривая оттока скважины (Справочник инженера-нефтяника. Том IV. Техника и технологии добычи. – М.-Ижевск: Институт компьютерных исследований, 2017. – xxxviii, 1191 c.) 
Сложность задачи связана с тем, что на работу скважины оказывает влияние большое количество факторов, которые не всегда возможно учесть и проводить их мониторинг на регулярной основе. 
Показатели работы скважин, получаемые с датчиков или вносимые в информационные системы людьми, могут содержать ошибки и пропуски, поэтому важное значение приобретает обработка данных и фильтрация выбросов (так называемые point outliers). 

1. Формат ввода
Вам предоставляются следующие файлы:
    • "train.csv" – файл с данными для обучения моделей.
Целевая переменная: "Забойное давление"
Характеристики тренировочной выборки:
    • Размер train-таблицы: 34300 строк на 6 столбцов
Столбец
Описание
WCT
Обводненность
THP
Устьевое давление
LIQ
Дебит жидкости
PUMP
Частота работы насоса ЭЦН
GOR
Газовый фактор
BHP
Забойное давление

1.2. Формат вывода
Ответ принимается в формате .csv. Ваша модель должна сформировать прогноз забойных давлений. Предсказания модели должны быть сформированы для файла val.csv. Пример генерации файла с ответом в базовом решении в файле "baseline_solution.ipynb".

Столбец
Описание
BHP
Забойное давление

1.3. Описание обозначений
ЭЦН – наиболее широко распространенный в России аппарат механизированной добычи нефти (ESP – electric submersible pump – погружной насос)

1.4. Комментарии и оценка решений
Ошибка прогноза будет оцениваться на отложенной выборке. Для оценки и ранжирования предлагаемых участниками моделей будет использоваться показатель MSE (Mean Square Error)

1.5. Идея решения
Базовое решение, основанное на оптимизации параметров, описывающих кривую падения дебита нефти, представлено в файле "baseline_solution.py". В этом решении для построения прогноза используются только предшествующие значения целевой переменной.
Подробнее о DCA (Decline Curve Analysis): https://petrowiki.spe.org/Production_forecasting_decline_curve_analysis.
Для решения задачи возможно использование любых моделей и подходов к решению задачи регрессии, в том числе алгоритмов AutoML, классических моделей МО, нейронных сетей. Участники могут использовать различные методы заполнения пропусков в данных либо не учитывать параметры, содержащие пропуски. Допускается построение моделей на основе любых наборов параметров, доступных в файле "train.csv".
