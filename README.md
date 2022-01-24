# AllAccess
A Xamarin Forms hub for accessibility features<br>


# AllAccess


## Abstract
With over 20% of Canadians being disabled [1] and 15% of the world’s population[2] having a disability, a large demographic exists that cannot fully carry out day-to-day tasks. Therefore, developing features to enable these people to fully interact with the world is important in removing the barriers they face. Accessibility is referred to as the presence of these features. Through technology, more accessibility features have been developed. However, while there has been a growth in the number of these features, they are not all being fully utilized. There’s the case of useful technologies that aid accessibility being available but not being used,  and even if used, being implemented poorly. Maybe these accessibility features are difficult to access as they are spread across multiple apps and platforms. This project aims to address these problems. It aims to better use the technology available to implement accessibility features. The main idea is to create a central location for various accessibility features that already exist. This central location will be a mobile application because it is the most portable means of technology. The end product of this project is a structure for which existing accessibility features will be located. 

                      
       

## Background

### Tools
I developed the project using Xamarin.Forms. Xamarin is a framework for developing mobile applications. It has the benefit of being a cross-platform development tool. This means that while other mobile development tools like Android Studio and Swift only allow you to develop for their respective platforms, either Android or IOS, Xamarin allows you to develop simultaneously for both platforms. 
In Xamarin, the logic of an app is written in the programming language C#, and the Markup language, XAML is used for designing the app. The software Visual Studio provides several features that are used to create, edit and debug Xamarin apps. The technical term for software like this is an IDE. The IDE Visual Studio was used to develop the project while I tested the app on both an android emulator and a Samsung phone.


### Software Architecture
The main architecture of the project is that each accessibility feature would be treated as an individual microservice that functions on its own. The primary interface of the app provides navigation to these microservices. This architecture means that each accessibility feature was independently developed and then linked to the main application. The aim of this is to meet the idea of a central location that connects distinct features. 

## Description

### Structure
The function of the app is to create a hub for accessibility features the current version has only an object and colour identifier available, however, more features are being worked on. The app has a landing page that displays information about the app.  This page then provides navigation to the list of features developed. 

##  Design of the hub

### Main page 
The design of the Mainpage consists of a grid that has two rows. The first row contains the background image and the second row has a carousel that swipes to show the description of the different features. Here using data binding to the features file, data stored about the features is displayed. When clicked the button on the carousel navigates to the Camera page

``` xaml

        <Grid RowDefinitions="*,Auto" BackgroundColor="BlanchedAlmond">
            <Image Grid.Row="0" 
                   VerticalOptions="Start"
                   Source="IMG_main.png" 
                   Aspect="AspectFit" />

            <CarouselView Grid.Row="1"
                          x:Name="carouse" 
                          HeightRequest="250" 
                          Margin="0,-35,0,0" >

                <CarouselView.ItemsLayout>
                    <LinearItemsLayout Orientation="Horizontal" 
                                       ItemSpacing="0"
                                       SnapPointsType="MandatorySingle" />
                </CarouselView.ItemsLayout>

                <CarouselView.ItemTemplate>
                    <DataTemplate>
                        <Grid>
                            <Frame CornerRadius="30" HasShadow="False" BackgroundColor="white" >
                                <Grid RowDefinitions="Auto,Auto,*">

                                    <Label  Grid.Row="0"
                                            LineHeight="1.5"
                                            FontAttributes="Bold" 
                                            VerticalOptions="Start" 
                                            HorizontalTextAlignment="Center"
                                            FontSize="Large"
                                            Text="{Binding description} "/>
                                    <Label Grid.Row="1" 
                                           Text="{Binding howTo} "                           
                                           FontAttributes="Bold" 
                                           TextColor="#9fa2a8" 
                                           FontSize="Medium"
                                           Margin="30,0"
                                           HorizontalTextAlignment="Center"/>

                            
                                    <Button Grid.Row="2" 
                                            BackgroundColor="Pink" 
                                            CornerRadius="33"
                                            HeightRequest="76"
                                            WidthRequest="76"
                                            ImageSource="{Binding icon}" 
                                            HorizontalOptions="Center"
                                            VerticalOptions="Center"
                                            Margin="0,0,0,15"
                                            Clicked="Button_Clicked"
                                            />
                                      </Grid>
                            </Frame>
                        </Grid>
                    </DataTemplate>
                </CarouselView.ItemTemplate>
            </CarouselView>
            <StackLayout Grid.Row="1" VerticalOptions="End" Orientation="Horizontal" HeightRequest="38">
                <Image x:Name="swipe"
                    Source="ICON_Swipe.png"
                    HorizontalOptions="EndAndExpand"
                    VerticalOptions="End"
                    Margin="0,0,10,0"
                    />
            </StackLayout>

        </Grid>
    </ContentPage.Content>
}

```
<img  src="https://user-images.githubusercontent.com/54193310/149999745-e589bcc2-278a-4867-b127-cedd6fc21ed1.png">



## Features page
The Camera Page is made using a stack layout[Figure E]. Stack Layout works by placing elements next to each other in one direction. This is similar to how stacks work, hence the name StackLayout. The Camera Page has two buttons that are stacked on each other and the background picture is displayed behind them in a lower opacity.
``` xaml 
<Grid>
            <StackLayout Orientation="Horizontal" 
                         HorizontalOptions="Center"
                         Padding="0" 
                         Spacing="0">
                <Image Source="IMG_Logoo.png" 
                       HorizontalOptions="Start"/>
                <Label Text="All Access!" 
                       HorizontalOptions="Center"
                       HorizontalTextAlignment="Start"
                       TextColor="White" 
                       FontAttributes="Bold" 
                       FontSize="Title"/>
            </StackLayout>
            <Frame CornerRadius="30" BackgroundColor="blanchedAlmond" >
            <Grid>
                <Image Source="IMG_main" Opacity="0.2">
                </Image>
                <CollectionView x:Name="lists"
                                Margin="0,60,0,0"
                                SelectionMode="Single"
                                SelectedItem="{Binding photo, Mode=TwoWay}"
                                SelectionChanged="Clicked">
                    <CollectionView.ItemsLayout>
                        <LinearItemsLayout Orientation="Vertical" ItemSpacing="12"/>
                    </CollectionView.ItemsLayout>
                    <CollectionView.ItemTemplate >
                        <DataTemplate>

                                <ContentView>
                                    <Frame BackgroundColor="White"  
                                           CornerRadius="15"
                                           IsClippedToBounds="True" 
                                           HeightRequest="110"
                                           Padding="10,6,10,0"
                                           HasShadow="False">
                                        <StackLayout Padding="0" >
                                        <Grid VerticalOptions="Start" >
                                            <Frame Padding="0" 
                                                   Margin="0"
                                                   CornerRadius="10">
                                                <Image Source="{Binding image}" 
                                                       Aspect="AspectFill" />
                                                </Frame>
                                        </Grid>
                                        <StackLayout VerticalOptions="EndAndExpand">
                                            <StackLayout Orientation="Horizontal">
                                                <Label Text="{Binding description}" 
                                                       HorizontalOptions="CenterAndExpand"
                                                       FontAttributes="Bold"
                                                       Margin="30,0,0,0"/>

                                                <Image Source="{Binding icon}" 
                                                   HorizontalOptions="EndAndExpand"
                                                   Margin="0,0,0,0"/>
                                            </StackLayout>

                                        </StackLayout>
                                    </StackLayout>
                                </Frame>
                                  
                                </ContentView>
                        </DataTemplate>
                    </CollectionView.ItemTemplate>
                </CollectionView>
            </Grid>
        </Frame>
            </Grid>
```  

![image](https://user-images.githubusercontent.com/54193310/149999894-ccce9da2-e021-4fcf-adf7-4ac94ec1a750.png)<br>

## Data/API

To achieve the current features(colour and object recognizer) Microsoft Cognitive Services is used. In microsoft azure I created a resource for this project.  This resource is the API the app uses to analyze images. These projects also contain the credentials and endpoints for the calls.  

In order to make the api call this code is used.
``` c#
 public static class Api
    {
        public static async Task<string> callApi(int type, string Key, string endpoint, Stream image)
        {
            HttpClient client = new HttpClient();
            client.DefaultRequestHeaders.Add("ocp-apim-subscription-key", Key);
            var requestUrl = "";
            switch (type)
            {
                case 1://color
                    requestUrl = $"{endpoint}/vision/v3.2/analyze?visualFeatures=Color&language=en&model-version=latest";
                    break;
                case 2://vision
                    requestUrl = $"{endpoint}/vision/v3.2/describe";
                    break;
            }
            //construct the api call
            var request = new HttpRequestMessage(HttpMethod.Post, endpoint);
            request.RequestUri = new Uri(requestUrl);

            //add the image to the request
            request.Content = new StreamContent(image);

            request.Content.Headers.ContentType = new MediaTypeHeaderValue("application/octet-stream");
            HttpResponseMessage responseMessage = new HttpResponseMessage();
            string result = "";
            //get the result from the api call
            try
            {
                responseMessage = await client.SendAsync(request);
            }
            catch (Exception ex)
            {
                displayException(ex);
            }
            if (responseMessage.IsSuccessStatusCode){
                if (responseMessage.Content != null)
                {
                    result = await responseMessage.Content.ReadAsStringAsync();
                    client.Dispose();
                    client = null;
                }
            }
            else
            {
            displayException(responseMessage);
            }
            
            return result;

        }
```  


## Version 2.0
In the projects current state it can identify colours present in an image and give its description. These features are intended to assist the colour blind in identifying colours and the visually impaired in identifying objects and describing their surroundings. I am currently integrating voice commands and augmented reality to increase the range of accesibility features.

## Appendix
[1]
E. and S. D. Canada, “Government of Canada,” Making an accessible Canada for people with disabilities - Canada.ca, 04-Jun-2021. [Online]. Available: https://www.canada.ca/en/employment-social-development/programs/accessible-canada.html. [Accessed: 05-Nov-2021]. 

[2]
 “Disability,” World Health Organization. [Online]. Available: https://www.who.int/health-topics/disability#tab=tab_1. 
[Accessed: 05-Nov-2021]. 

 
