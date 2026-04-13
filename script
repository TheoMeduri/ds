const root = document.documentElement;
const themeToggle = document.getElementById("themeToggle");
const openModalBtn = document.getElementById("openModalBtn");
const closeModalBtn = document.getElementById("closeModalBtn");
const cancelModalBtn = document.getElementById("cancelModalBtn");
const modalBackdrop = document.getElementById("modalBackdrop");
const toastBtn = document.getElementById("toastBtn");
const toastStack = document.getElementById("toastStack");

const savedTheme = localStorage.getItem("ekolyra-theme");
if (savedTheme) {
  root.setAttribute("data-theme", savedTheme);
}

themeToggle?.addEventListener("click", () => {
  const current = root.getAttribute("data-theme");
  const next = current === "dark" ? "light" : "dark";
  root.setAttribute("data-theme", next);
  localStorage.setItem("ekolyra-theme", next);
});

function openModal() {
  modalBackdrop.classList.add("open");
  document.body.style.overflow = "hidden";
}

function closeModal() {
  modalBackdrop.classList.remove("open");
  document.body.style.overflow = "";
}

openModalBtn?.addEventListener("click", openModal);
closeModalBtn?.addEventListener("click", closeModal);
cancelModalBtn?.addEventListener("click", closeModal);

modalBackdrop?.addEventListener("click", (e) => {
  if (e.target === modalBackdrop) closeModal();
});

document.addEventListener("keydown", (e) => {
  if (e.key === "Escape") {
    closeModal();
    closeAllDropdowns();
    closeAllSelects();
  }
});

function createToast(title, message) {
  const toast = document.createElement("div");
  toast.className = "toast glass";
  toast.innerHTML = `
    <strong>${title}</strong>
    <p>${message}</p>
  `;
  toastStack.appendChild(toast);

  setTimeout(() => {
    toast.style.opacity = "0";
    toast.style.transform = "translateY(10px)";
    setTimeout(() => toast.remove(), 250);
  }, 2800);
}

toastBtn?.addEventListener("click", () => {
  closeModal();
  createToast("Salvo com sucesso", "A ação foi concluída no sistema visual Ekolyra.");
});

/* Custom Select */
const selects = document.querySelectorAll("[data-select]");

function closeAllSelects() {
  selects.forEach((select) => select.classList.remove("open"));
}

selects.forEach((select) => {
  const trigger = select.querySelector(".select-trigger");
  const options = select.querySelectorAll(".select-option");
  const value = select.querySelector(".select-value");
  const hiddenInput = select.querySelector('input[type="hidden"]');

  trigger?.addEventListener("click", (e) => {
    e.stopPropagation();
    const isOpen = select.classList.contains("open");
    closeAllSelects();
    if (!isOpen) select.classList.add("open");
  });

  options.forEach((option) => {
    option.addEventListener("click", () => {
      const label = option.textContent.trim();
      const optionValue = option.dataset.value || label;

      value.textContent = label;
      hiddenInput.value = optionValue;
      select.classList.remove("open");
    });
  });
});

/* Tabs */
const tabsGroups = document.querySelectorAll("[data-tabs]");

tabsGroups.forEach((tabs) => {
  const buttons = tabs.querySelectorAll(".tab-btn");
  const panels = tabs.querySelectorAll(".tab-panel");

  buttons.forEach((button) => {
    button.addEventListener("click", () => {
      const target = button.dataset.tab;

      buttons.forEach((btn) => btn.classList.remove("active"));
      panels.forEach((panel) => panel.classList.remove("active"));

      button.classList.add("active");
      tabs.querySelector(`#${target}`)?.classList.add("active");
    });
  });
});

/* Accordion */
const accordions = document.querySelectorAll("[data-accordion]");

accordions.forEach((accordion) => {
  const items = accordion.querySelectorAll(".accordion-item");

  items.forEach((item) => {
    const trigger = item.querySelector(".accordion-trigger");

    trigger?.addEventListener("click", () => {
      const isActive = item.classList.contains("active");

      items.forEach((i) => i.classList.remove("active"));
      if (!isActive) item.classList.add("active");
    });
  });
});

/* Dropdown */
const dropdowns = document.querySelectorAll("[data-dropdown]");

function closeAllDropdowns() {
  dropdowns.forEach((dropdown) => dropdown.classList.remove("open"));
}

dropdowns.forEach((dropdown) => {
  const trigger = dropdown.querySelector(".dropdown-trigger");

  trigger?.addEventListener("click", (e) => {
    e.stopPropagation();
    const isOpen = dropdown.classList.contains("open");
    closeAllDropdowns();
    if (!isOpen) dropdown.classList.add("open");
  });
});

document.addEventListener("click", () => {
  closeAllDropdowns();
  closeAllSelects();
});

/* Demo dropdown item feedback */
document.querySelectorAll(".dropdown-item").forEach((item) => {
  item.addEventListener("click", () => {
    createToast("Menu acionado", `Você clicou em "${item.textContent.trim()}".`);
    closeAllDropdowns();
  });
});
