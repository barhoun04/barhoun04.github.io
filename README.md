<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Organigrama Interactivo del Sector Hostelero</title>
<style>
  body {
    font-family: 'Poppins', sans-serif;
    background: linear-gradient(135deg, #eef6ff, #dbeafe);
    margin: 0;
    padding: 40px;
    color: #1e3a8a;
  }

  h1 {
    text-align: center;
    color: #1e40af;
    margin-bottom: 40px;
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    gap: 30px;
  }

  .area {
    background: white;
    border-radius: 16px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    padding: 25px;
    cursor: pointer;
    transition: all 0.3s ease;
  }

  .area:hover { transform: translateY(-3px); }

  .area h2 {
    color: #1e3a8a;
    margin: 0;
    font-size: 1.4rem;
  }

  .area-desc {
    font-size: 0.95rem;
    color: #333;
    margin-top: 8px;
  }

  .jerarquia {
    margin-top: 15px;
    display: none;
    overflow-x: auto;
    padding-bottom: 15px;
  }

  .nivel {
    display: flex;
    flex-direction: column;
    gap: 15px;
    margin: 10px 0;
    padding-left: 20px;
    border-left: 2px solid #bfdbfe;
  }

  .nivel[data-nivel="1"] { margin-left: 0; border-color: #1e3a8a; }
  .nivel[data-nivel="2"] { margin-left: 40px; border-color: #1d4ed8; }
  .nivel[data-nivel="3"] { margin-left: 80px; border-color: #3b82f6; }
  .nivel[data-nivel="4"] { margin-left: 120px; border-color: #60a5fa; }
  .nivel[data-nivel="5"] { margin-left: 160px; border-color: #93c5fd; }

  .puesto {
    background: #eff6ff;
    border-radius: 12px;
    padding: 10px 14px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.05);
    cursor: pointer;
    transition: all 0.3s ease;
  }

  .puesto:hover { background: #dbeafe; }

  .puesto strong { display: block; color: #1e40af; font-weight: 600; font-size: 1rem; }

  .desc {
    display: none;
    font-size: 0.9rem;
    color: #333;
    margin-top: 6px;
    line-height: 1.4;
  }

  footer {
    text-align: center;
    margin-top: 50px;
    font-size: 0.85rem;
    color: #555;
    font-style: italic;
  }
</style>
</head>
<body>

<h1>Organigrama Interactivo del Sector Hostelero</h1>
<div class="container" id="areasContainer"></div>
<footer>Hecho por <strong>Mohamed Barhoun</strong></footer>

<script>
document.addEventListener("DOMContentLoaded", () => {
  const data = [
    {
      area: "Área 1 — Atención al cliente y gestión",
      descripcion: "Gestiona la recepción, administración, caja y atención al cliente.",
      jerarquia: [
        { nivel: 1, puesto: "Director / Gerente", desc: "Supervisa todas las áreas del restaurante y toma decisiones estratégicas." },
        { nivel: 2, puesto: "Jefe de Restaurante o Sala", desc: "Coordina el personal de sala y se encarga del servicio al cliente." },
        { nivel: 3, puesto: "Jefe de Recepción", desc: "Gestiona la entrada de clientes, reservas y flujo general de visitas." },
        { nivel: 4, puesto: "Recepcionista / Hostess", desc: "Atiende y recibe a los clientes, asigna mesas y gestiona reservas." },
        { nivel: 5, puesto: "Ayudante de Recepción", desc: "Apoya en la atención y gestiones administrativas de recepción." },
        { nivel: 3, puesto: "Jefe de Administración", desc: "Controla la facturación, nóminas y procesos contables." },
        { nivel: 4, puesto: "Administrativo", desc: "Realiza tareas contables, de archivo y documentación." },
        { nivel: 5, puesto: "Cajero", desc: "Gestiona cobros, devoluciones y arqueos de caja." }
      ]
    },
    {
      area: "Área 2 — Cocina y economato",
      descripcion: "Encargada de la elaboración de alimentos, control de calidad, almacenamiento y gestión de víveres.",
      jerarquia: [
        { nivel: 1, puesto: "Jefe de Cocina", desc: "Responsable máximo de la cocina, diseña menús y controla la calidad." },
        { nivel: 2, puesto: "Segundo Jefe de Cocina", desc: "Sustituye al jefe y coordina partidas y preparación." },
        { nivel: 3, puesto: "Jefe de Partida", desc: "Encargado de una sección específica (pescados, carnes, postres...)."},
        { nivel: 4, puesto: "Cocinero", desc: "Elabora platos según las recetas del establecimiento." },
        { nivel: 5, puesto: "Ayudante de Cocina", desc: "Asiste en tareas básicas y mantenimiento del orden." },
        { nivel: 2, puesto: "Encargado de Economato", desc: "Controla los inventarios y las compras de materia prima." },
        { nivel: 3, puesto: "Ayudante de Economato", desc: "Ayuda en el almacenamiento y organización de productos." }
      ]
    },
    {
      area: "Área 3 — Restaurante, bar y servicios similares",
      descripcion: "Responsable del servicio de comidas y bebidas, atención al cliente y gestión de eventos o catering.",
      jerarquia: [
        { nivel: 1, puesto: "Jefe de Sala", desc: "Coordina el personal de servicio y garantiza la atención adecuada." },
        { nivel: 2, puesto: "Jefe de Rango", desc: "Responsable de un grupo de mesas o zona concreta del comedor." },
        { nivel: 3, puesto: "Camarero", desc: "Atiende mesas, toma pedidos y sirve comidas y bebidas." },
        { nivel: 4, puesto: "Ayudante de Camarero", desc: "Apoya a los camareros en montaje, limpieza y reposición." },
        { nivel: 2, puesto: "Sumiller", desc: "Selecciona vinos, asesora al cliente y gestiona la bodega." },
        { nivel: 2, puesto: "Barman", desc: "Elabora cócteles, gestiona el bar y atiende a los clientes." },
        { nivel: 3, puesto: "Ayudante de Bar", desc: "Apoya en limpieza, reposición y preparación de bebidas." }
      ]
    },
    {
      area: "Área 4 — Pisos y limpieza",
      descripcion: "Mantiene el orden, limpieza y cuidado de mobiliario en todas las áreas del establecimiento.",
      jerarquia: [
        { nivel: 1, puesto: "Gobernanta / Jefe de Pisos", desc: "Dirige el equipo de limpieza y controla el estado de las zonas comunes." },
        { nivel: 2, puesto: "Encargado de Sección", desc: "Coordina grupos de limpieza y distribuye tareas." },
        { nivel: 3, puesto: "Camarero/a de Pisos", desc: "Limpia habitaciones, áreas comunes y reemplaza textiles." },
        { nivel: 4, puesto: "Auxiliar de Limpieza", desc: "Apoya en lavandería y limpieza general." }
      ]
    },
    {
      area: "Área 5 — Mantenimiento y servicios auxiliares",
      descripcion: "Encargada del mantenimiento técnico, reparaciones y conservación de maquinaria e instalaciones.",
      jerarquia: [
        { nivel: 1, puesto: "Encargado de Mantenimiento", desc: "Planifica revisiones técnicas y gestiona reparaciones." },
        { nivel: 2, puesto: "Especialista de Mantenimiento", desc: "Ejecuta reparaciones técnicas eléctricas o mecánicas." },
        { nivel: 3, puesto: "Ayudante de Mantenimiento", desc: "Apoya en mantenimiento preventivo y pequeños arreglos." },
        { nivel: 4, puesto: "Auxiliar de Servicios", desc: "Realiza tareas logísticas y de soporte general." }
      ]
    },
    {
      area: "Área 6 — Ocio y bienestar",
      descripcion: "Ofrece actividades recreativas, deportivas, termales y de bienestar complementarias al servicio principal.",
      jerarquia: [
        { nivel: 1, puesto: "Responsable de Ocio y Animación", desc: "Planifica y supervisa actividades recreativas y deportivas." },
        { nivel: 2, puesto: "Coordinador de Actividades", desc: "Gestiona equipos y asegura la correcta ejecución de programas." },
        { nivel: 3, puesto: "Técnico de Spa / Termal", desc: "Opera equipos y aplica tratamientos de bienestar." },
        { nivel: 4, puesto: "Personal de Belleza y Estética", desc: "Realiza tratamientos estéticos y de cuidado personal." },
        { nivel: 5, puesto: "Personal de Salud y Bienestar", desc: "Proporciona masajes, terapias y atención física relajante." }
      ]
    }
  ];

  const container = document.getElementById("areasContainer");

  data.forEach(area => {
    const div = document.createElement("div");
    div.className = "area";
    div.innerHTML = `<h2>${area.area}</h2><div class="area-desc">${area.descripcion}</div>`;

    const jerDiv = document.createElement("div");
    jerDiv.className = "jerarquia";

    // Agrupar por nivel
    const niveles = {};
    area.jerarquia.forEach(p => {
      if (!niveles[p.nivel]) niveles[p.nivel] = [];
      niveles[p.nivel].push(p);
    });

    Object.keys(niveles).sort().forEach(n => {
      const nivelDiv = document.createElement("div");
      nivelDiv.className = "nivel";
      nivelDiv.dataset.nivel = n;
      niveles[n].forEach(p => {
        const puestoDiv = document.createElement("div");
        puestoDiv.className = "puesto";
        puestoDiv.innerHTML = `<strong>${p.puesto}</strong><span class="desc">${p.desc}</span>`;
        puestoDiv.addEventListener("click", e => {
          e.stopPropagation();
          const desc = puestoDiv.querySelector(".desc");
          desc.style.display = desc.style.display === "block" ? "none" : "block";
        });
        nivelDiv.appendChild(puestoDiv);
      });
      jerDiv.appendChild(nivelDiv);
    });

    div.appendChild(jerDiv);
    div.addEventListener("click", () => {
      jerDiv.style.display = jerDiv.style.display === "block" ? "none" : "block";
    });

    container.appendChild(div);
  });
});
</script>

</body>
</html>
