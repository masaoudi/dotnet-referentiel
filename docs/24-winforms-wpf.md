# 🪟 WinForms & WPF

Applications desktop.

## WinForms

Framework UI Windows **classique**.

### Caractéristiques

- Designer drag & drop
- Événements (Click, Load)
- Contrôles : Button, TextBox, DataGrid

### Exemple

```csharp
private void btnSubmit_Click(object sender, EventArgs e)
{
    MessageBox.Show($"Bonjour {txtName.Text}");
}
```

## WPF

Framework UI **moderne**.

### Caractéristiques

- **XAML** pour l'interface
- **Data binding** puissant
- Styles et templates
- **MVVM** (Model-View-ViewModel)
- Animations, graphiques vectoriels

### Exemple XAML

```xml
<Window x:Class="MyApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation">
    <StackPanel>
        <TextBox Text="{Binding UserName}" />
        <Button Content="Cliquer" Command="{Binding SubmitCommand}" />
    </StackPanel>
</Window>
```

### MVVM

```csharp
public class MainViewModel : INotifyPropertyChanged
{
    private string _userName;
    public string UserName
    {
        get => _userName;
        set
        {
            _userName = value;
            OnPropertyChanged();
        }
    }

    public ICommand SubmitCommand { get; }

    public MainViewModel()
    {
        SubmitCommand = new RelayCommand(Submit);
    }

    private void Submit() { /* ... */ }

    public event PropertyChangedEventHandler PropertyChanged;
    protected void OnPropertyChanged([CallerMemberName] string name = null)
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(name));
    }
}
```

## Comparaison

| Critère | WinForms | WPF |
|---------|:--------:|:---:|
| Âge | Ancien | Moderne |
| Design | Drag & drop | XAML |
| Data binding | Basique | Puissant |
| MVVM | ❌ | ✅ |
| Animations | ❌ | ✅ |

## DevExpress

Suite de **composants UI** premium.

- Grilles, charts, rapports
- WinForms + WPF
- Utilisé chez ODDO BHF