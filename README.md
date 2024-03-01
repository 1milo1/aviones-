# aviones- Definición de la clase Aviones
class Aviones:
    def __init__(self, marca, modelo, capacidad_pasajeros):
        self.marca = marca
        self.modelo = modelo
        self.capacidad_pasajeros = capacidad_pasajeros

    def despegar(self):
        return f"{self.modelo} de {self.marca} despegando."

    def aterrizar(self):
        return f"{self.modelo} de {self.marca} aterrizando."

# Herencia 1: AvionComercial
class AvionComercial(Aviones):
    def __init__(self, marca, modelo, capacidad_pasajeros, aerolinea):
        super().__init__(marca, modelo, capacidad_pasajeros)
        self.aerolinea = aerolinea

    def anunciar(self):
        return f"Bienvenidos al vuelo de {self.modelo} de {self.marca}, operado por {self.aerolinea}."

# Herencia 2: AvionCarga
class AvionCarga(Aviones):
    def __init__(self, marca, modelo, capacidad_pasajeros, capacidad_carga_kg):
        super().__init__(marca, modelo, capacidad_pasajeros)
        self.capacidad_carga_kg = capacidad_carga_kg

    def cargar(self):
        return f"{self.modelo} de {self.marca} siendo cargado con {self.capacidad_carga_kg} kg de carga."

# Herencia 3: AvionPrivado
class AvionPrivado(Aviones):
    def __init__(self, marca, modelo, capacidad_pasajeros, propietario):
        super().__init__(marca, modelo, capacidad_pasajeros)
        self.propietario = propietario

    def informacion_propietario(self):
        return f"Este {self.modelo} de {self.marca} pertenece a {self.propietario}."

# Polimorfismo
def ejecutar_despegue(atributo_despegue):
    return atributo_despegue.despegar()

# Creación de instancias
avion_comercial = AvionComercial("Boeing", "737", 150, "American Airlines")
avion_carga = AvionCarga("Airbus", "A380", 0, 250000)
avion_privado = AvionPrivado("Cessna", "Citation X", 8, "John Doe")

from flask import Flask, jsonify, request

app = Flask(__name__)

@app.route('/login', methods=['POST'])
def login():
    # Aquí iría la lógica de autenticación
    data = request.get_json()
    username = data.get('username')
    password = data.get('password')

    # Ejemplo básico de autenticación
    if username == 'admin' and password == 'password':
        return jsonify({'message': 'Login successful!'})
    else:
        return jsonify({'message': 'Invalid credentials'}), 401

@app.route('/clientes')
def gestion_clientes():
    # Aquí iría la lógica para obtener y gestionar clientes
    clientes = [
        {'id': 1, 'nombre': 'Cliente 1'},
        {'id': 2, 'nombre': 'Cliente 2'}
    ]
    return jsonify(clientes)

if __name__ == '__main__':
    app.run(debug=True)

    import React, { useState } from 'react';
import axios from 'axios';

const Login = () => {
  const [username, setUsername] = useState('');
  const [password, setPassword] = useState('');
  const [message, setMessage] = useState('');

  const handleSubmit = async (e) => {
    e.preventDefault();
    try {
      const response = await axios.post('http://localhost:5000/login', { username, password });
      setMessage(response.data.message);
    } catch (error) {
      setMessage('Error: Invalid credentials');
    }
  };

  return (
    <div>
      <h2>Login</h2>
      <form onSubmit={handleSubmit}>
        <input type="text" placeholder="Username" value={username} onChange={(e) => setUsername(e.target.value)} />
        <input type="password" placeholder="Password" value={password} onChange={(e) => setPassword(e.target.value)} />
        <button type="submit">Login</button>
      </form>
      <p>{message}</p>
    </div>
  );
};

export default Login;

import React, { useState, useEffect } from 'react';
import axios from 'axios';

const GestionCliente = () => {
  const [clientes, setClientes] = useState([]);

  useEffect(() => {
    const fetchClientes = async () => {
      try {
        const response = await axios.get('http://localhost:5000/clientes');
        setClientes(response.data);
      } catch (error) {
        console.error('Error fetching clientes:', error);
      }
    };
    fetchClientes();
  }, []);

  return (
    <div>
      <h2>Gestión de Clientes</h2>
      <ul>
        {clientes.map((cliente) => (
          <li key={cliente.id}>{cliente.nombre}</li>
        ))}
      </ul>
    </div>
  );
};

export default GestionCliente;

git branch develop
git checkout develop

git add .
git commit -m "Initial commit"

git push origin develop
