/**
 * Proyecto SENA - Ficha 3186597
 * Módulo: Diseño y codificación de servicios web
 * Descripción: Servidor base en Node.js y Express para la gestión de servicios de la aplicación.
 */

const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;

// Middleware para parsear JSON en las peticiones HTTP
app.use(express.json());

/**
 * @route GET /api/status
 * @desc Endpoint de verificación del estado del servicio web
 */
app.get('/api/status', (req, res) => {
    res.status(200).json({
        status: "success",
        message: "Servicio web operando correctamente",
        timestamp: new Date()
    });
});

/**
 * @route POST /api/data
 * @desc Endpoint para recibir y registrar información del sistema
 */
app.post('/api/data', (req, res) => {
    const payload = req.body;
    
    // Validación básica de datos de entrada
    if (!payload || Object.keys(payload).length === 0) {
        return res.status(400).json({
            error: "El cuerpo de la petición no puede estar vacío"
        });
    }

    res.status(201).json({
        message: "Datos recibidos y almacenados con éxito",
        data: payload
    });
});

// Inicialización del servidor escuchando en el puerto configurado
app.listen(PORT, () => {
    console.log(`Servidor ejecutándose en el puerto ${PORT}`);
});
