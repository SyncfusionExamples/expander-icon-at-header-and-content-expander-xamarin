# How to display the expander icon in the header at collapsed state and content at expand state in Xamarin.Forms Expander (SfExpander)

You can customize the expander icon to be in header or content based on expand/collapse by using custom expander icon and [converters](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/data-binding/converters) in Xamarin.Forms [SfExpander](https://help.syncfusion.com/xamarin/expander/getting-started).

You can refer to the following document to use custom font icons in SfExpander from the following link,

[https://www.syncfusion.com/kb/11469/how-to-use-a-custom-font-icon-for-expander-in-xamarin-forms-sfexpander](https://www.syncfusion.com/kb/11469/how-to-use-a-custom-font-icon-for-expander-in-xamarin-forms-sfexpander)

You can also refer the following article.

https://www.syncfusion.com/kb/11919/how-to-display-the-expander-icon-in-the-header-at-collapsed-state-and-content-at-expand

**XAML**

Define converters for [Expander.Header](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.Expander.XForms~Syncfusion.XForms.Expander.SfExpander~Header.html) and [Expander.Content](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.Expander.XForms~Syncfusion.XForms.Expander.SfExpander~Content.html) to change the expander icon visibility based on [IsExpanded](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.Expander.XForms~Syncfusion.XForms.Expander.SfExpander~IsExpanded.html) property.

``` xml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:ExpanderXamarin"
             xmlns:syncfusion="clr-namespace:Syncfusion.XForms.Expander;assembly=Syncfusion.Expander.XForms"
             x:Class="ExpanderXamarin.MainPage" Padding="{OnPlatform iOS='0,40,0,0'}">
    <ContentPage.Resources>
        <ResourceDictionary>
            <OnPlatform x:TypeArguments="x:String" x:Key="ExpanderIcon">
                <On Platform="Android" Value="ExpanderIcons.ttf#ExpanderIcons" />
                <On Platform="UWP" Value="/Assets/ExpanderIcons.ttf#ExpanderIcons" />
                <On Platform="iOS" Value="ExpanderIcons" />
            </OnPlatform>
        </ResourceDictionary>
        <local:ExpanderIconConverter x:Key="ExpanderIconConverter"/>
        <local:ExpanderVisibilityConverter x:Key="ExpanderVisibilityConverter"/>
    </ContentPage.Resources>
    <ContentPage.Content>
        <ScrollView BackgroundColor="#EDF2F5" Margin="{OnPlatform iOS='0,40,0,0'}">
            <StackLayout>
                <syncfusion:SfExpander x:Name="expander1" HeaderIconPosition="None">
                    <syncfusion:SfExpander.Header>
                        <Grid HeightRequest="50">
                            <Grid.ColumnDefinitions>
                                <ColumnDefinition Width="50"/>
                                <ColumnDefinition Width="*"/>
                            </Grid.ColumnDefinitions>
                            <Label HorizontalOptions="Center" VerticalOptions="Center"
                                FontFamily="{StaticResource ExpanderIcon}"
                                IsVisible="{Binding Path=IsExpanded, Source={x:Reference expander1}, Converter={StaticResource ExpanderVisibilityConverter}, ConverterParameter=Header}" 
                                Text="{Binding Path=IsExpanded,Source={x:Reference expander1}, Converter={StaticResource ExpanderIconConverter}, ConverterParameter={x:Static Device.RuntimePlatform}}"/>
                            <Label Text="Veg Pizza" Grid.Column="1" TextColor="#495F6E"  VerticalTextAlignment="Center" />
                        </Grid>
                    </syncfusion:SfExpander.Header>
                    <syncfusion:SfExpander.Content>
                        <Grid BackgroundColor="#FFFFFF">
                            <Grid.ColumnDefinitions>
                                <ColumnDefinition Width="50"/>
                                <ColumnDefinition Width="*"/>
                            </Grid.ColumnDefinitions>
                            <Label HorizontalOptions="Center" VerticalOptions="Center"
                                   FontFamily="{StaticResource ExpanderIcon}" 
                                   IsVisible="{Binding Path=IsExpanded,Source={x:Reference expander1}, Converter={StaticResource ExpanderVisibilityConverter}, ConverterParameter=Content}" 
                                   Text="{Binding Path=IsExpanded,Source={x:Reference expander1}, Converter={StaticResource ExpanderIconConverter}, ConverterParameter={x:Static Device.RuntimePlatform}}"/>
                            <Label BackgroundColor="#FFFFFF" HeightRequest="50" Grid.Column="1" Text="Veg pizza is prepared with the items that meet vegetarian standards by not including any meat or animal tissue products." TextColor="#303030" VerticalTextAlignment="Center"/>
                        </Grid>
                    </syncfusion:SfExpander.Content>
                </syncfusion:SfExpander>
            </StackLayout>
        </ScrollView>
    </ContentPage.Content>
</ContentPage>
```
**C#**

Returns true or false, based on the expanded state for both **Header** and **Content**.

``` c#
public class ExpanderVisibilityConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        if ((string)parameter == "Header")
            return (bool)value ? false : true;
        else
            return (bool)value ? true : false;
    }

    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        throw new NotImplementedException();
    }
}
```
**Output**

![ExpanderHeaderContent](https://github.com/SyncfusionExamples/expander-icon-at-header-and-content-expander-xamarin/blob/master/ScreenShot/ExpanderHeaderContent.gif)
