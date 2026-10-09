import streamlit as st
import pandas as pd
import plotly.express as px

# Настройка страницы
st.set_page_config(
    page_title="Лабораторный портфель проектов",
    page_icon="📊",
    layout="wide"
)

st.title("📊 Дорожная карта и диаграмма Ганта проектов лаборатории")
st.markdown("Интерактивный дашборд ключевых вех, задач и сроков (2025–2027 гг.)")

# 1. Данные по проектам
@st.cache_data
def load_data():
    raw_tasks = [
        # DEV
        {"ID": "DEV005", "Project": "DEV005 Герминальный sm-ngp", "Task": "Sample Report модули", "Start": "2026-01-01", "End": "2026-04-30", "Group": "DEV", "Lead": "Сафин Э.Ф."},
        {"ID": "DEV005", "Project": "DEV005 Герминальный sm-ngp", "Task": "Апдейтер референсов & Распределенный пайплайн", "Start": "2026-05-01", "End": "2026-08-31", "Group": "DEV", "Lead": "Сафин Э.Ф."},
        {"ID": "DEV005", "Project": "DEV005 Герминальный sm-ngp", "Task": "SamoVarACMG CNV & Рефакторинг аннотации", "Start": "2026-07-01", "End": "2026-10-15", "Group": "DEV", "Lead": "Сафин Э.Ф."},
        {"ID": "DEV005", "Project": "DEV005 Герминальный sm-ngp", "Task": "Релиз v3 (документация и сдача)", "Start": "2026-10-01", "End": "2026-11-30", "Group": "DEV", "Lead": "Сафин Э.Ф."},
        {"ID": "DEV007", "Project": "DEV007 СППВР Orpheus", "Task": "Распил кода и интеграция БД аллелей", "Start": "2026-01-01", "End": "2026-04-30", "Group": "DEV", "Lead": "Альберт Е.А."},
        {"ID": "DEV007", "Project": "DEV007 СППВР Orpheus", "Task": "Интеграция сложных генов & Документация", "Start": "2026-03-01", "End": "2026-09-30", "Group": "DEV", "Lead": "Альберт Е.А."},
        {"ID": "DEV007", "Project": "DEV007 СППВР Orpheus", "Task": "Сдача кода и досье на тех. испытания", "Start": "2026-05-01", "End": "2026-10-15", "Group": "DEV", "Lead": "Альберт Е.А."},
        {"ID": "DEV008", "Project": "DEV008 База Euridice", "Task": "Релизы v0.1 (28 генов) - v0.2 (82 гена)", "Start": "2026-01-01", "End": "2026-07-31", "Group": "DEV", "Lead": "Эсибов А.А."},
        {"ID": "DEV008", "Project": "DEV008 База Euridice", "Task": "Релизы v0.3 (259 генов) - v0.4 (334 гена)", "Start": "2026-06-01", "End": "2026-10-15", "Group": "DEV", "Lead": "Эсибов А.А."},
        {"ID": "DEV008", "Project": "DEV008 База Euridice", "Task": "Регистрация БД каузативных вариантов", "Start": "2026-06-01", "End": "2026-10-31", "Group": "DEV", "Lead": "Эсибов А.А."},
        {"ID": "DEV008", "Project": "DEV008 База Euridice", "Task": "Финальный релиз v1.0.0", "Start": "2026-10-01", "End": "2026-12-31", "Group": "DEV", "Lead": "Эсибов А.А."},
        {"ID": "DEV009", "Project": "DEV009 Типирование ВГР", "Task": "AmpliconPipe: фазирование, статья, диссертация", "Start": "2026-01-01", "End": "2026-06-30", "Group": "DEV", "Lead": "Антышева З.Г."},
        {"ID": "DEV009", "Project": "DEV009 Типирование ВГР", "Task": "HHRTyper v2.1 и v3", "Start": "2026-05-01", "End": "2026-11-15", "Group": "DEV", "Lead": "Антышева З.Г."},
        {"ID": "DEV009", "Project": "DEV009 Типирование ВГР", "Task": "Драфт статьи HHRTyper", "Start": "2026-09-01", "End": "2026-12-31", "Group": "DEV", "Lead": "Антышева З.Г."},
        {"ID": "DEV010", "Project": "DEV010 Биоинформатик Эвоген", "Task": "Этапы I-III контракта (сдача 25.09)", "Start": "2026-01-01", "End": "2026-09-25", "Group": "DEV", "Lead": "Альберт Е.А."},
        {"ID": "DEV010", "Project": "DEV010 Биоинформатик Эвоген", "Task": "POC галоса, импутация и статья НИПТ", "Start": "2026-01-01", "End": "2026-11-30", "Group": "DEV", "Lead": "Альберт Е.А."},
        {"ID": "DEV011", "Project": "DEV011 LP-Test DM1", "Task": "POC импутации полигенных скоров DM1", "Start": "2026-01-01", "End": "2026-07-01", "Group": "DEV", "Lead": "Альберт Е.А."},
        {"ID": "DEV011", "Project": "DEV011 LP-Test DM1", "Task": "Драфт статьи HLA-риск vs LP", "Start": "2026-05-01", "End": "2026-09-01", "Group": "DEV", "Lead": "Табаков Д.В."},
        {"ID": "DEV012", "Project": "DEV012 ПО O-APP", "Task": "Релизы v1.0, v1.2, v1.3 (таблицы)", "Start": "2026-01-01", "End": "2026-06-30", "Group": "DEV", "Lead": "Рогаткин М.Д."},
        {"ID": "DEV012", "Project": "DEV012 ПО O-APP", "Task": "Релиз core-api v2.0 (08.10.2026)", "Start": "2026-05-01", "End": "2026-10-08", "Group": "DEV", "Lead": "Рогаткин М.Д."},
        {"ID": "DEV013", "Project": "DEV013 ИАС клиники", "Task": "БД, API стенд и конструктор форм (Этапы 1-2)", "Start": "2025-12-01", "End": "2026-05-31", "Group": "DEV", "Lead": "Терехова А.С."},
        {"ID": "DEV013", "Project": "DEV013 ИАС клиники", "Task": "Запуск версий v1 и v2 ИАС (Этап 3)", "Start": "2026-04-01", "End": "2026-09-30", "Group": "DEV", "Lead": "Терехова А.С."},
        {"ID": "DEV013", "Project": "DEV013 ИАС клиники", "Task": "Релиз модуля Биобанк v1.0 (15.10.2026)", "Start": "2026-01-01", "End": "2026-10-15", "Group": "DEV", "Lead": "Терехова А.С."},
        # CLI
        {"ID": "CLI001", "Project": "CLI001 СД1 генетический", "Task": "Контракты Инвитро и регионы", "Start": "2025-12-01", "End": "2026-06-30", "Group": "CLI", "Lead": "Михальков С.Н."},
        {"ID": "CLI001", "Project": "CLI001 СД1 генетический", "Task": "Открытие баз: МОНИКИ, КГМУ, Амурская ГМА", "Start": "2026-01-01", "End": "2026-05-31", "Group": "CLI", "Lead": "Михальков С.Н."},
        {"ID": "CLI001", "Project": "CLI001 СД1 генетический", "Task": "Набор 1000 - 2000 участников", "Start": "2026-01-01", "End": "2026-12-31", "Group": "CLI", "Lead": "Михальков С.Н."},
        {"ID": "CLI003", "Project": "CLI003 KCNV2 обсервация", "Task": "Набор пациентов в клиниках РФ", "Start": "2026-01-01", "End": "2026-12-31", "Group": "CLI", "Lead": "Антонова А."},
        {"ID": "CLI003", "Project": "CLI003 KCNV2 обсервация", "Task": "Интеграция Китая / Грант РФ-Китай", "Start": "2026-05-01", "End": "2026-09-30", "Group": "CLI", "Lead": "Антонова А."},
        {"ID": "CLI004", "Project": "CLI004 Моногенные 36+", "Task": "Открытие центров (ЭНЦ, КГМУ, НГМУ, ОДКБ)", "Start": "2026-01-01", "End": "2026-05-31", "Group": "CLI", "Lead": "Михальков С.Н."},
        {"ID": "CLI004", "Project": "CLI004 Моногенные 36+", "Task": "Включение 600 - 1200 участников", "Start": "2026-01-01", "End": "2026-12-31", "Group": "CLI", "Lead": "Михальков С.Н."},
        {"ID": "CLI006", "Project": "CLI006 ДКИ ВДКН", "Task": "POC: разведение мышей, препарат, эксперимент", "Start": "2026-01-01", "End": "2026-12-31", "Group": "CLI", "Lead": "Антонова А."},
        {"ID": "CLI006", "Project": "CLI006 ДКИ ВДКН", "Task": "ДКИ: программа НЦЭСМП, масштабирование", "Start": "2026-04-01", "End": "2026-11-30", "Group": "CLI", "Lead": "Антонова А."},
        {"ID": "CLI007", "Project": "CLI007 ДКИ KCNV2", "Task": "POC: AAV8 vs 3g6 и финальный препарат", "Start": "2026-01-01", "End": "2026-12-31", "Group": "CLI", "Lead": "Антонова А."},
        {"ID": "CLI007", "Project": "CLI007 ДКИ KCNV2", "Task": "Пилот на приматах Saifu & VectorBuilder", "Start": "2026-04-01", "End": "2027-01-31", "Group": "CLI", "Lead": "Антонова А."},
        {"ID": "CLI007", "Project": "CLI007 ДКИ KCNV2", "Task": "Согласование ДКИ НЦЭСМП и выбор центра", "Start": "2026-08-01", "End": "2026-12-31", "Group": "CLI", "Lead": "Антонова А."},
        {"ID": "CLI008", "Project": "CLI008 СД1 динамический", "Task": "Включение участников на 2-ю точку (183/300)", "Start": "2026-01-01", "End": "2026-12-31", "Group": "CLI", "Lead": "Фролова Т.М."},
        {"ID": "CLI008", "Project": "CLI008 СД1 динамический", "Task": "Публикации и доклады по модели манифестации", "Start": "2026-07-01", "End": "2026-12-31", "Group": "CLI", "Lead": "Фролова Т.М."},
        {"ID": "CLI010", "Project": "CLI010 Регистрация Orpheus", "Task": "Тех. испытания во ВНИИИМТ", "Start": "2026-01-01", "End": "2026-06-30", "Group": "CLI", "Lead": "Неверова Д."},
        {"ID": "CLI010", "Project": "CLI010 Регистрация Orpheus", "Task": "Клинические испытания (КИ)", "Start": "2026-07-01", "End": "2026-12-31", "Group": "CLI", "Lead": "Неверова Д."},
        {"ID": "CLI011", "Project": "CLI011 Регистрация Колибри", "Task": "Документация и договор ВНИИИМТ", "Start": "2026-02-01", "End": "2026-07-31", "Group": "CLI", "Lead": "Неверова Д."},
        {"ID": "CLI011", "Project": "CLI011 Регистрация Колибри", "Task": "Тех. испытания и подача досье в РЗН", "Start": "2026-08-01", "End": "2026-12-31", "Group": "CLI", "Lead": "Неверова Д."},
        # FAC
        {"ID": "FAC003", "Project": "FAC003 Клонирование", "Task": "Размер генов 2-3 кб & Golden Gate", "Start": "2026-03-01", "End": "2026-10-31", "Group": "FAC", "Lead": "Никитина М.А."},
        {"ID": "FAC009", "Project": "FAC009 Секвенирование", "Task": "Валидация E+75, ФКУ и Oxford Nanopore", "Start": "2026-03-01", "End": "2026-10-31", "Group": "FAC", "Lead": "Степанова А.А."},
        {"ID": "FAC012", "Project": "FAC012 IT-инфраструктура", "Task": "Slurm-кластер, self-hosted GitLab, серверы", "Start": "2026-01-01", "End": "2026-11-30", "Group": "FAC", "Lead": "Горелышев А.С."},
        {"ID": "FAC016", "Project": "FAC016 Биобанк", "Task": "СОПы, к.303 МФТИ и выбор ЛИС", "Start": "2026-01-01", "End": "2026-09-30", "Group": "FAC", "Lead": "Марков А.В."},
        {"ID": "FAC016", "Project": "FAC016 Биобанк", "Task": "Внедрение ЛИС и миграция данных", "Start": "2026-09-01", "End": "2027-03-31", "Group": "FAC", "Lead": "Марков А.В."},
        {"ID": "FAC017", "Project": "FAC017 Single cell & Spatial", "Task": "Visium HD (НЭО ПЖ, надпочечники), AAV сетчатки", "Start": "2026-01-01", "End": "2026-06-30", "Group": "FAC", "Lead": "Кацаран Ю."},
        {"ID": "FAC019", "Project": "FAC019 mAb фасилити", "Task": "mAb к CD4, TRBV20, биспецифик CD16, TRBV-платформа", "Start": "2026-01-01", "End": "2026-09-01", "Group": "FAC", "Lead": "Софронова Е.В."},
        {"ID": "FAC023", "Project": "FAC023 Патоморфология", "Task": "Протоколы гистологии и сервисы (Фабри, ФКУ, MODY10)", "Start": "2026-05-16", "End": "2027-02-28", "Group": "FAC", "Lead": "Емелин А."},
        {"ID": "FAC025", "Project": "FAC025 Метаболомика", "Task": "Методики ВЭЖХ-МС, Sciex 6500+, стероиды", "Start": "2026-08-01", "End": "2026-12-01", "Group": "FAC", "Lead": "Нестеров М.С."},
        {"ID": "FAC026", "Project": "FAC026 Синтез олиго", "Task": "Оснащение лаборатории и регулярный синтез", "Start": "2026-06-01", "End": "2026-12-31", "Group": "FAC", "Lead": "Сеферян М.А."},
        # SCI & EDU
        {"ID": "SCI022", "Project": "SCI022 Кластеризация СД1", "Task": "Кластеризация v2.0 (low PRS) и v3.0 (TCR)", "Start": "2026-01-01", "End": "2026-12-31", "Group": "SCI", "Lead": "Табаков Д.В."},
        {"ID": "SCI024", "Project": "SCI024 CASP2 эструс мышей", "Task": "Статьи по мышиному эструсу и CASP2", "Start": "2026-02-01", "End": "2026-11-30", "Group": "SCI", "Lead": "Антышева З.Г."},
        {"ID": "SCI027", "Project": "SCI027/28 TCR/BCR ДНКseq", "Task": "Скрининг лимфом, клеточные линии, 2 MVP коробки", "Start": "2026-04-01", "End": "2026-12-31", "Group": "SCI", "Lead": "Табаков Д.В."},
        {"ID": "SCI029", "Project": "SCI029 TCR терапия", "Task": "Отработка ADCC in vitro (aTRBV20, aCD4)", "Start": "2026-07-01", "End": "2026-10-01", "Group": "SCI", "Lead": "Ишина И.А."},
        {"ID": "SCI030", "Project": "SCI030 TCR валидация/TCR-T", "Task": "Валидация TCR & Портфель k562 с HLA", "Start": "2026-01-01", "End": "2026-05-31", "Group": "SCI", "Lead": "Ишина И.А."},
        {"ID": "SCI033", "Project": "SCI033 Ревматоидный артрит", "Task": "Single-cell синовия, набор 1000 РА когорты", "Start": "2026-01-01", "End": "2027-03-31", "Group": "SCI", "Lead": "Астахова Е.А."},
        {"ID": "SCI034", "Project": "SCI034 CGP онкотест WES", "Task": "Биомаркерная БД, соматический пайплайн, MVP", "Start": "2026-01-01", "End": "2026-12-31", "Group": "SCI", "Lead": "Кремлёв А."},
        {"ID": "SCI035", "Project": "SCI035 PAM50 онкотест", "Task": "RNA-seq наборы, RepGen сервис, MVP конвейер", "Start": "2026-01-01", "End": "2026-12-31", "Group": "SCI", "Lead": "Кремлёв А."},
        {"ID": "SCI042", "Project": "SCI042 Гормонотерапия РМЖ", "Task": "Дизайн опухолевой модели и договор с клиникой", "Start": "2026-05-01", "End": "2026-12-31", "Group": "SCI", "Lead": "Момчева Р."},
        {"ID": "SCI043", "Project": "SCI043 НЭО ПЖ bulk RNAseq", "Task": "Архивные FFPE, секвенирование и риск метастазирования", "Start": "2026-01-01", "End": "2026-12-31", "Group": "SCI", "Lead": "Максимов Д.О."},
        {"ID": "SCI044", "Project": "SCI044 Опухоли надпочечников", "Task": "Stereo-seq валидация и публикация (с ЭНЦ)", "Start": "2026-01-01", "End": "2026-08-31", "Group": "SCI", "Lead": "Максимов Д.О."},
        {"ID": "EDU002", "Project": "EDU002 Биоинф. школа 2026", "Task": "Организация, программа, проведение школы", "Start": "2026-03-01", "End": "2026-08-17", "Group": "EDU", "Lead": "Блинова И.Р."},
    ]
    df = pd.DataFrame(raw_tasks)
    df["Start"] = pd.to_datetime(df["Start"])
    df["End"] = pd.to_datetime(df["End"])
    return df

df = load_data()

# 2. Боковая панель фильтров
st.sidebar.header("Фильтры отображения")

all_groups = sorted(df["Group"].unique().tolist())
selected_groups = st.sidebar.multiselect(
    "Направления проектов:",
    options=all_groups,
    default=all_groups
)

filtered_df = df[df["Group"].isin(selected_groups)]

all_projects = sorted(filtered_df["Project"].unique().tolist())
selected_projects = st.sidebar.multiselect(
    "Конкретные проекты:",
    options=all_projects,
    default=all_projects
)

filtered_df = filtered_df[filtered_df["Project"].isin(selected_projects)]

# Фильтр по датам
min_date = df["Start"].min().to_pydatetime()
max_date = df["End"].max().to_pydatetime()
date_range = st.sidebar.date_input(
    "Диапазон дат:",
    value=(min_date, max_date),
    min_value=min_date,
    max_value=max_date
)

if len(date_range) == 2:
    start_d, end_d = pd.to_datetime(date_range[0]), pd.to_datetime(date_range[1])
    filtered_df = filtered_df[(filtered_df["End"] >= start_d) & (filtered_df["Start"] <= end_d)]

# Метрики в верхней панели
col1, col2, col3 = st.columns(3)
col1.metric("Всего активных проектов в выборке", filtered_df["ID"].nunique())
col2.metric("Количество вех / задач", len(filtered_df))
col3.metric("Выбранные группы", ", ".join(selected_groups) if selected_groups else "—")

# 3. Отрисовка диаграммы Ганта
if not filtered_df.empty:
    colors = {
        "DEV": "#1f77b4",  # Синий
        "CLI": "#2ca02c",  # Зеленый
        "FAC": "#ff7f0e",  # Оранжевый
        "SCI": "#d62728",  # Красный
        "EDU": "#9467bd",  # Фиолетовый
    }

    fig = px.timeline(
        filtered_df,
        x_start="Start",
        x_end="End",
        y="Project",
        color="Group",
        text="Task",
        hover_data={"ID": True, "Lead": True, "Start": True, "End": True},
        color_discrete_map=colors,
        category_orders={"Project": list(reversed(filtered_df["Project"].unique().tolist()))}
    )

    fig.update_yaxes(autorange="reversed")
    fig.update_layout(
        height=max(500, len(filtered_df["Project"].unique()) * 35),
        xaxis_title="Месяцы и Годы",
        yaxis_title="Проект",
        font=dict(size=11),
        xaxis=dict(tickformat="%b %Y", dtick="M1", showgrid=True),
        hoverlabel=dict(bgcolor="white", font_size=12),
        margin=dict(l=10, r=10, t=30, b=10)
    )

    st.plotly_chart(fig, use_container_width=True)

    # 4. Сводная таблица данных
    with st.expander("📋 Посмотреть данные в виде таблицы"):
        display_df = filtered_df[["ID", "Project", "Group", "Lead", "Task", "Start", "End"]].copy()
        display_df["Start"] = display_df["Start"].dt.strftime("%Y-%m-%d")
        display_df["End"] = display_df["End"].dt.strftime("%Y-%m-%d")
        st.dataframe(display_df, use_container_width=True, hide_index=True)
        
        csv = display_df.to_csv(index=False).encode('utf-8-sig')
        st.download_button(
            label="📥 Скачать план в формате CSV",
            data=csv,
            file_name="lab_projects_gantt.csv",
            mime="text/csv"
        )
else:
    st.warning("Нет задач, соответствующих выбранным фильтрам.")
