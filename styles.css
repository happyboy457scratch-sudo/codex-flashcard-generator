const loginForm = document.getElementById('login-form');
const usernameInput = document.getElementById('username-input');
const passwordInput = document.getElementById('password-input');

const topicForm = document.getElementById('topic-form');
const countForm = document.getElementById('count-form');
const topicInput = document.getElementById('topic-input');
const countInput = document.getElementById('count-input');
const countTopicText = document.getElementById('count-topic-text');

const loginScreen = document.getElementById('login-screen');
const topicScreen = document.getElementById('topic-screen');
const countScreen = document.getElementById('count-screen');
const flashcardScreen = document.getElementById('flashcard-screen');

const cardQuestion = document.getElementById('card-question');
const cardAnswer = document.getElementById('card-answer');
const cardFront = document.getElementById('card-front');
const cardBack = document.getElementById('card-back');
const flipBtn = document.getElementById('flip-btn');

const progressText = document.getElementById('progress-text');
const backBtn = document.getElementById('back-btn');
const nextBtn = document.getElementById('next-btn');
const finishedState = document.getElementById('finished-state');
const flashcard = document.getElementById('flashcard');
const restartBtn = document.getElementById('restart-btn');
const newTopicBtn = document.getElementById('new-topic-btn');

let selectedTopic = '';
let flashcards = [];
let currentIndex = 0;
let showingFinished = false;
let isFlipped = false;

const topicKnowledge = {
  photosynthesis: [
    { question: 'What is photosynthesis?', answer: 'Photosynthesis is the process plants use to convert light energy, water, and carbon dioxide into glucose and oxygen.' },
    { question: 'Where does photosynthesis happen in a plant cell?', answer: 'It occurs in chloroplasts, especially in leaf cells.' },
    { question: 'What is the main pigment used in photosynthesis?', answer: 'Chlorophyll is the primary pigment that captures light energy.' },
    { question: 'What are the two major stages of photosynthesis?', answer: 'The light-dependent reactions and the Calvin cycle (light-independent reactions).' },
    { question: 'Why is photosynthesis important for life on Earth?', answer: 'It produces oxygen and forms the base of many food chains by creating energy-rich molecules.' }
  ],
  'world war ii': [
    { question: 'When did World War II begin and end?', answer: 'It began in 1939 and ended in 1945.' },
    { question: 'What event triggered World War II in Europe?', answer: 'Germany invaded Poland in September 1939.' },
    { question: 'Who were the major Allied powers?', answer: 'The United States, the Soviet Union, the United Kingdom, and China were key Allied powers.' },
    { question: 'What was D-Day?', answer: 'D-Day was the Allied invasion of Normandy on June 6, 1944.' },
    { question: 'How did World War II end in the Pacific?', answer: 'After atomic bombs were dropped on Hiroshima and Nagasaki, Japan surrendered in August 1945.' }
  ],
  javascript: [
    { question: 'What is JavaScript commonly used for?', answer: 'It is used to add interactivity and dynamic behavior to web pages.' },
    { question: 'What is the difference between let and const?', answer: 'Both are block-scoped, but const cannot be reassigned after declaration.' },
    { question: 'What is an array in JavaScript?', answer: 'An array is an ordered collection that can store multiple values in a single variable.' },
    { question: 'What is a function?', answer: 'A function is a reusable block of code that performs a task and can return a value.' },
    { question: 'What does JSON stand for?', answer: 'JSON stands for JavaScript Object Notation, a text format for data exchange.' }
  ]
};

function normalizeTopic(topic) {
  return topic.trim().toLowerCase();
}

function generateFallbackFlashcards(topic) {
  return [
    { question: `What is ${topic}?`, answer: `${topic} is the topic you requested. Start by defining its core idea in one sentence.` },
    { question: `Why is ${topic} important?`, answer: `Think about where ${topic} appears in real life and why people study or use it.` },
    { question: `What are the key parts of ${topic}?`, answer: `Break ${topic} into 3-5 subtopics and learn each one separately.` },
    { question: `What is one common misunderstanding about ${topic}?`, answer: `Identify a frequent misconception and explain the correct idea in your own words.` },
    { question: `How would you teach ${topic} to someone else?`, answer: `Teaching ${topic} aloud is a fast way to check if you really understand it.` }
  ];
}

function getFlashcardsForTopic(topic) {
  const normalized = normalizeTopic(topic);
  if (topicKnowledge[normalized]) return topicKnowledge[normalized];
  if (normalized.includes('wwii') || normalized.includes('world war 2')) return topicKnowledge['world war ii'];
  if (normalized.includes('javascript')) return topicKnowledge.javascript;
  return generateFallbackFlashcards(topic.trim());
}

function buildDeck(topic, count) {
  const source = getFlashcardsForTopic(topic);
  const deck = [];
  for (let i = 0; i < count; i += 1) {
    deck.push(source[i % source.length]);
  }
  return deck;
}

function showOnlyScreen(target) {
  loginScreen.classList.remove('active');
  topicScreen.classList.remove('active');
  countScreen.classList.remove('active');
  flashcardScreen.classList.remove('active');
  target.classList.add('active');
}

function showFront() {
  isFlipped = false;
  cardFront.classList.remove('hidden');
  cardBack.classList.add('hidden');
  flipBtn.textContent = 'Flip Card';
}

function showBack() {
  isFlipped = true;
  cardFront.classList.add('hidden');
  cardBack.classList.remove('hidden');
  flipBtn.textContent = 'Show Question';
}

function renderCard() {
  const card = flashcards[currentIndex];
  cardQuestion.textContent = card.question;
  cardAnswer.textContent = card.answer;
  progressText.textContent = `Card ${currentIndex + 1} of ${flashcards.length}`;
  backBtn.disabled = currentIndex === 0;
  nextBtn.textContent = currentIndex === flashcards.length - 1 ? 'Finish ▶' : 'Next ▶';
  showFront();
}

function showFinished() {
  showingFinished = true;
  flashcard.classList.add('hidden');
  flipBtn.classList.add('hidden');
  finishedState.classList.remove('hidden');
  progressText.textContent = `Completed ${flashcards.length} of ${flashcards.length} cards`;
  backBtn.disabled = false;
  nextBtn.disabled = true;
}

function hideFinished() {
  showingFinished = false;
  flashcard.classList.remove('hidden');
  flipBtn.classList.remove('hidden');
  finishedState.classList.add('hidden');
  nextBtn.disabled = false;
}

loginForm.addEventListener('submit', (event) => {
  event.preventDefault();
  const username = usernameInput.value.trim();
  const password = passwordInput.value.trim();

  if (!username || !password) {
    return;
  }

  showOnlyScreen(topicScreen);
  topicInput.focus();
});

topicForm.addEventListener('submit', (event) => {
  event.preventDefault();
  const topic = topicInput.value.trim();
  if (!topic) return;

  selectedTopic = topic;
  countTopicText.textContent = `Topic: ${selectedTopic}`;
  countInput.value = '';
  showOnlyScreen(countScreen);
  countInput.focus();
});

countForm.addEventListener('submit', (event) => {
  event.preventDefault();
  const count = Number(countInput.value);

  if (!Number.isInteger(count) || count < 1 || count > 20) {
    countInput.setCustomValidity('Please choose a whole number from 1 to 20.');
    countInput.reportValidity();
    return;
  }

  countInput.setCustomValidity('');
  flashcards = buildDeck(selectedTopic, count);
  currentIndex = 0;
  hideFinished();
  renderCard();
  showOnlyScreen(flashcardScreen);
});

flipBtn.addEventListener('click', () => {
  if (isFlipped) {
    showFront();
  } else {
    showBack();
  }
});

backBtn.addEventListener('click', () => {
  if (showingFinished) {
    hideFinished();
    currentIndex = flashcards.length - 1;
    renderCard();
    return;
  }

  if (currentIndex > 0) {
    currentIndex -= 1;
    renderCard();
  }
});

nextBtn.addEventListener('click', () => {
  if (showingFinished) return;

  if (currentIndex < flashcards.length - 1) {
    currentIndex += 1;
    renderCard();
  } else {
    showFinished();
  }
});

restartBtn.addEventListener('click', () => {
  hideFinished();
  currentIndex = 0;
  renderCard();
});

newTopicBtn.addEventListener('click', () => {
  showOnlyScreen(topicScreen);
  topicInput.focus();
});
