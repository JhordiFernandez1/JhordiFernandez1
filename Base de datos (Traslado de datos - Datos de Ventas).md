//Hoja de Ventas

function trasladarDatos() {
  // Obtener la hoja de cálculo activa
  var ss = SpreadsheetApp.getActiveSpreadsheet();

  // Obtener las hojas de trabajo
  var hojaOrigen = ss.getSheetByName("Datos de prospectos");
  var hojaDestino = ss.getSheetByName("Datos de Ventas");

  // Obtener los datos de la hoja de origen
  var datosOrigen = hojaOrigen.getDataRange().getValues();

  // Obtener la última fila con datos en la hoja de destino
  var ultimaFila = hojaDestino.getLastRow();

  // Array para almacenar los datos a trasladar
  var datosATrasladar = [];

  // Recorrer los datos de origen
  for (var i = 0; i < datosOrigen.length; i++) {
    var fila = datosOrigen[i];
    var columnaR = fila[17]; // Columna R (índice 17)

    // Verificar si el valor de la columna R cumple con las condiciones
    if (columnaR === "Firmado" || columnaR === "Postulando" || columnaR === "Aceptado" ||
        columnaR === "Rechazado" || columnaR === "Se retiró" || columnaR === "En Canadá") {

      // Obtener los valores de las columnas A, C, D, R y V
      var columnaA = fila[0]; // Columna A (índice 0)
      var columnaC = fila[2]; // Columna C (índice 2)
      var columnaD = fila[3]; // Columna D (índice 3)
      var columnaV = fila[21]; // Columna V (índice 21)

      // Crear un array con los datos a trasladar
      var datosFila = [columnaA, columnaC, columnaD, columnaR, columnaV];

      // Agregar los datos al array de datos a trasladar
      datosATrasladar.push(datosFila);
    }
  }

  // Escribir los datos en la hoja de destino a partir de la fila 2
  hojaDestino.getRange(2, 1, datosATrasladar.length, datosATrasladar[0].length).setValues(datosATrasladar);
}
