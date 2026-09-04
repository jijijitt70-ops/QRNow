document.addEventListener("DOMContentLoaded", () => {

  const typeButtons = document.querySelectorAll(".type-btn");

  const inputs = {
    url: document.getElementById("url-input"),
    text: document.getElementById("text-input"),
    phone: document.getElementById("phone-input"),
    email: document.getElementById("email-input"),
    wifi: document.getElementById("wifi-input")
  };

  const generateButton = document.getElementById("generate-btn");
  const downloadButton = document.getElementById("download-btn");

  const qrContainer = document.getElementById("qr-container");
  const status = document.getElementById("status");

  const qrColor = document.getElementById("qr-color");
  const bgColor = document.getElementById("bg-color");

  const qrColorValue = document.getElementById("qr-color-value");
  const bgColorValue = document.getElementById("bg-color-value");

  const qrSize = document.getElementById("qr-size");
  const sizeValue = document.getElementById("size-value");

  let currentType = "url";
  let hasQR = false;


  // CAMBIAR TIPO DE QR

  typeButtons.forEach(button => {

    button.addEventListener("click", () => {

      typeButtons.forEach(btn => {
        btn.classList.remove("active");
      });

      button.classList.add("active");

      currentType = button.dataset.type;

      Object.values(inputs).forEach(input => {
        input.classList.add("hidden");
      });

      inputs[currentType].classList.remove("hidden");

      status.textContent = "Listo para generar";

    });

  });


  // COLORES

  qrColor.addEventListener("input", () => {
    qrColorValue.textContent = qrColor.value.toUpperCase();
  });

  bgColor.addEventListener("input", () => {
    bgColorValue.textContent = bgColor.value.toUpperCase();
  });


  // TAMAÑO

  qrSize.addEventListener("input", () => {
    sizeValue.textContent = `${qrSize.value}px`;
  });


  // OBTENER INFORMACIÓN

  function getContent() {

    if (currentType === "url") {

      const value = document.getElementById("url").value.trim();

      if (!value) return null;

      return value;
    }


    if (currentType === "text") {

      const value = document.getElementById("text").value.trim();

      if (!value) return null;

      return value;
    }


    if (currentType === "phone") {

      const value = document.getElementById("phone").value.trim();

      if (!value) return null;

      return `tel:${value}`;
    }


    if (currentType === "email") {

      const value = document.getElementById("email").value.trim();

      if (!value) return null;

      return `mailto:${value}`;
    }


    if (currentType === "wifi") {

      const name = document
        .getElementById("wifi-name")
        .value
        .trim();

      const password = document
        .getElementById("wifi-password")
        .value
        .trim();

      const security = document
        .getElementById("wifi-security")
        .value;

      if (!name) return null;

      return `WIFI:T:${security};S:${escapeWifi(name)};P:${escapeWifi(password)};;`;
    }

    return null;
  }


  // ESCAPAR DATOS WIFI

  function escapeWifi(value) {

    return value
      .replace(/\\/g, "\\\\")
      .replace(/;/g, "\\;")
      .replace(/,/g, "\\,")
      .replace(/:/g, "\\:");

  }


  // GENERAR QR

  function generateQR() {

    const content = getContent();

    if (!content) {

      status.textContent = "Falta información";

      alert("Introduce la información que quieres convertir en QR.");

      return;
    }


    if (typeof QRCode === "undefined") {

      status.textContent = "Cargando...";

      setTimeout(generateQR, 500);

      return;
    }


    qrContainer.innerHTML = "";


    new QRCode(qrContainer, {

      text: content,

      width: Number(qrSize.value),

      height: Number(qrSize.value),

      colorDark: qrColor.value,

      colorLight: bgColor.value,

      correctLevel: QRCode.CorrectLevel.H

    });


    hasQR = true;

    downloadButton.disabled = false;

    status.textContent = "QR generado ✓";

  }


  // BOTÓN GENERAR

  generateButton.addEventListener("click", generateQR);


  // DESCARGAR QR

  downloadButton.addEventListener("click", () => {

    if (!hasQR) return;

    const canvas = qrContainer.querySelector("canvas");
    const image = qrContainer.querySelector("img");


    if (canvas) {

      const link = document.createElement("a");

      link.download = "codigo-qr.png";

      link.href = canvas.toDataURL("image/png");

      link.click();

      return;
    }


    if (image) {

      const link = document.createElement("a");

      link.download = "codigo-qr.png";

      link.href = image.src;

      link.click();

    }

  });


  // ENTER PARA GENERAR

  document.getElementById("url").addEventListener("keydown", event => {

    if (event.key === "Enter") {
      generateQR();
    }

  });


  document.getElementById("text").addEventListener("keydown", event => {

    if (event.ctrlKey && event.key === "Enter") {
      generateQR();
    }

  });


  // REGENERAR AL CAMBIAR PERSONALIZACIÓN

  qrColor.addEventListener("change", () => {

    if (hasQR) {
      generateQR();
    }

  });


  bgColor.addEventListener("change", () => {

    if (hasQR) {
      generateQR();
    }

  });


  qrSize.addEventListener("change", () => {

    if (hasQR) {
      generateQR();
    }

  });

});
