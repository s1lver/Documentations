+++
title = "Расширение запечатанных классов"

[menu.main]
identifier = "sealed_class_extension"
parent = "bestpractices"
+++


Мы обратили внимание на то, что некоторые из наших разработчиков модификаций запрашивают обходной путь для расширения запечатанных классов. В этой статье мы рассмотрим, почему в игровых кодах есть запечатанные классы и как добиться для них расширенного поведения.

Одна из основных причин, по которой мы сделали фундаментальные классы запечатанными, — это позволить кодовой базе поддерживать широкий спектр модов которые могут работать одновременно с максимальной эффективностью. Для этого и в соответствии с принципами программной инженерии мы рекомендуем создавать моды как автономные, модульные расширения кода, такие как Campaign Behaviors, Game Models и пользовательские классы или компоненты, которые можно добавлять или удалять без каких-либо осложнений. Наследование от основных классов кампании увеличивает вероятность конфликтов с другими модами и будущими официальными обновлениями из-за изменения иерархии классов и может привести к индивидуальным изменениям фундаментальной логики игры. Хотя можно написать аккуратный код, который избегает этих проблем, мы решили придерживаться этих стандартов в нашей кодовой базе и полностью снизить вероятность конфликта из внутренних или внешних источников.

Когда дело доходит до достижения расширенного поведения для запечатанных классов без наследования, хотя можно изучить различные обходные пути, одно из возможных решений обсуждается ниже.

По сути, когда проблема расширения запечатанных классов решена, необходимо решить два основных требования, а именно: добавление нового поведения и добавление новых свойств.

Чтобы добавить новое поведение к запечатанным классам, можно использовать функцию C#, называемую «extension methods». Вкратце, это позволяет добавлять новые методы к любому классу, не создавая новый тип или не изменяя исходный. За подробной информации обратитесь к [руководству](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/extension-methods).

Добавление нового свойства может быть достигнуто путем связывания экземпляра запечатанного класса с соответствующим значением свойства с помощью словаря. В сочетании с методами расширения запечатанный класс может предоставить интерфейс для нового свойства, как если бы оно было добавлено непосредственно в класс.

```C#
    public class HeroManaExtensionCampaignBehavior : CampaignBehaviorBase
    {
        private Dictionary<Hero, float> _heroManaValues = new Dictionary<Hero, float>();
    
        public float GetMana(Hero hero)
        {
            if(_heroManaValues.TryGetValue(hero, out float result))
            {
                return result;
            }            
        
            return 0; //default value
        }

        public void SetMana(Hero hero, float newValue)
        {
            _heroManaValues[hero] = newValue;
        }

        public override void RegisterEvents(){ }        
        public override void SyncData(IDataStore dataStore)
        {
            dataStore.SyncData("_heroManaValues", ref _heroManaValues);
        }
    }

    public static class HeroManaExtensions
    {         
        public static float GetMana(this Hero hero)
        {
            var behavior = Campaign.Current.GetCampaignBehavior<HeroManaExtensionCampaignBehavior >();
            return behavior.GetMana(hero);
        }

        public static void SetMana(this Hero hero, float newMana)
        {
            var behavior = Campaign.Current.GetCampaignBehavior<HeroManaExtensionCampaignBehavior >();

            behavior.SetMana(hero, newMana);
        }
    }

```

Хотя это решение представляет собой жизнеспособный обходной путь для расширения запечатанных классов, важно помнить, что каждый проект имеет разные требования, и, следовательно, вам следует изучить, какой подход лучше всего подходит для вашего кода. 