О проекте

Russian: Практическая реализация Retrieval-Augmented Generation (RAG) для создания локальной базы знаний корпоративных документов. Проект решает проблему «галлюцинаций» ИИ, привязывая ответы модели к вашим внутренним инструкциям.

English: A practical implementation of Retrieval-Augmented Generation (RAG) to build a secure, local knowledge base for corporate documents. This project solves the AI "Hallucination" problem by grounding the model in your internal instructions.

🛠 Технологии (Tech Stack)

Russian:

Embedding: sentence-transformers (мультиязычная модель).
База данных: ChromaDB (локальная, Persistent).
Среда: Google Colab / Jupyter.

English:

Embedding: sentence-transformers (Multilingual).
Vector DB: ChromaDB (Local/Persistent).
Environment: Google Colab / Jupyter.
🏗 Архитектура и процесс (Architecture & Workflow)

Russian:

Чанкинг (Chunking): Большие документы разбиваются на мелкие фрагменты (чанки), чтобы сохранить смысл.
Векторизация: Каждый фрагмент превращается в математический вектор (Embedding).
Хранение: Векторы сохраняются в локальную папку chroma_db.
Поиск (Retriever): Запрос пользователя векторизуется, и система ищет 3 самых похожих вектора.
Генерация: Найденный текст передается в LLM как контекст.

English:

Chunking: Raw documents are split into small pieces to preserve semantic meaning.
Embedding: Each chunk is converted into a mathematical vector.
Storage: Vectors are saved to a local chroma_db folder.
Retrieval: User query is vectorized; system searches for Top-3 similar vectors.
Generation: Found text is passed as Context to the LLM.
📊 Результаты и выводы (Results & Key Findings)

Russian:

✅ Успех (Семантика): Модель понимает смысл. Запрос «Как оформить отпуск?» нашел инструкцию «Пишет заявление за 14 дней», хотя слова разные.
⚠️ Риск (Галлюцинации): На вопрос, которого нет в базе (например, «Как уволить?»), модель нашла инструкцию про «Отпуск». Вывод: Без проверки (Self-Correction) LLM придумает ответ, основываясь на найденном мусоре.
✅ Двуязычие: Модель paraphrase-multilingual успешно работает с RU и EN в одной базе.

English:

✅ Success (Semantic Search): The model understands meaning. Query "Vacation" found "Submit written request 14 days in advance".
⚠️ Risk (Hallucination): When asked about "Firing" (not in DB), it retrieved "Vacation" chunks. Lesson: RAG will hallucinate if the Retriever finds irrelevant data.
✅ Bilingual: The multilingual model handles both RU and EN queries in a single vector space.
▶️ Запуск (Setup & Usage)

Russian:

Установка: !pip install sentence-transformers chromadb tqdm
Запуск блоков: Выполните блоки 1–4 для создания базы. Блок 5 — для тестов.

English:

Install: !pip install sentence-transformers chromadb tqdm
Run: Execute Blocks 1-4 to create the DB. Block 5 for testing.
🚀 Дальнейшие шаги (Next Steps)

Russian: Для решения проблемы из Теста 2 и 4 необходимо внедрить Agentic RAG:

Re-Ranker: Пересортировать найденные документы по релевантности.
Self-Correction: Если уверенность модели низкая, отвечать: «В базе знаний нет информации по этому запросу».

English: To fix the Hallucination issue found in Tests 2 & 4, implement Agentic RAG:

Re-Ranker: Re-sort retrieved docs by relevance score.
Self-Correction: If confidence is low, reply: "I found info on X, but have no data on your specific query."
