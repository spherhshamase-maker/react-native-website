import React, { useState } from 'react';
import { Text, View, FlatList, TouchableOpacity, TextInput, Button } from 'react-native';

export default function App() {
  const [businesses, setBusinesses] = useState([
    { id: '1', name: 'Durban Barber', category: 'Beauty', phone: '0712345678' },
    { id: '2', name: 'Street Food Spot', category: 'Food', phone: '0723456789' },
  ]);

  const [name, setName] = useState('');
  const [category, setCategory] = useState('');
  const [phone, setPhone] = useState('');

  const addBusiness = () => {
    if (!name || !category || !phone) return;

    setBusinesses([
      ...businesses,
      { id: Date.now().toString(), name, category, phone }
    ]);

    setName('');
    setCategory('');
    setPhone('');
  };

  return (
    <View style={{ padding: 20, marginTop: 40 }}>
      <Text style={{ fontSize: 24, fontWeight: 'bold' }}>Work App</Text>

      <Text style={{ marginTop: 20 }}>Add Business</Text>
      <TextInput placeholder="Name" value={name} onChangeText={setName} style={{ borderWidth: 1, marginBottom: 10 }} />
      <TextInput placeholder="Category" value={category} onChangeText={setCategory} style={{ borderWidth: 1, marginBottom: 10 }} />
      <TextInput placeholder="Phone" value={phone} onChangeText={setPhone} style={{ borderWidth: 1, marginBottom: 10 }} />

      <Button title="Add" onPress={addBusiness} />

      <Text style={{ marginTop: 20, fontSize: 18 }}>Businesses</Text>

      <FlatList
        data={businesses}
        keyExtractor={(item) => item.id}
        renderItem={({ item }) => (
          <TouchableOpacity
            onPress={() => {
              const url = `https://wa.me/${item.phone}`;
              Linking.openURL(url);
            }}
          >
            <View style={{ padding: 10, borderBottomWidth: 1 }}>
              <Text>{item.name}</Text>
              <Text>{item.category}</Text>
            </View>
          </TouchableOpacity>
        )}
      />
    </View>
  );
}
