# Requirement-5
using System;

namespace Requirement5
{
    class Program
    {
        static void Main(string[] args)
        {
            int noOfStories;
            string storyDetails;
            Console.WriteLine("Enter no of stores:");
            noOfStories = Convert.ToInt32(Console.ReadLine());
            NoOfReadsComparator noOfReadsComparator = new NoOfReadsComparator();
            Story[] storyDetailsArray = new Story[noOfStories];


            for (int i = 0; i < noOfStories; i++)
            {
                Console.WriteLine("Enter the details of story {0}:", i + 1);
                storyDetails = Console.ReadLine();

                storyDetailsArray[i] = StoryBo.createStory(storyDetails);
            }

            Console.WriteLine("Press 1->View By Authou Name 2->View By Likes");
            int choice = Convert.ToInt32(Console.ReadLine());

            switch (choice)
            {
                case 1:
                    Console.WriteLine("Sorted By Name:");
                    Array.Sort(storyDetailsArray);
                    break;
                case 2:
                    Console.WriteLine("Sorted By No Of Reads:");
                    Array.Sort(storyDetailsArray, noOfReadsComparator);
                    break;
                default:
                    Console.WriteLine("Invalid Choice!..");
                    break;
            }

            foreach (Story st in storyDetailsArray)
            {
                Console.WriteLine(st);
            }

        }
    }
}


//story class

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Requirement5
{
    class Story : IComparable
    {
        private string name, authorName, genre;
        private int noOfChapters, noOfLikes, noOfReads;

        public Story(string name, string authorName, string genre, int noOfChapters, int noOfLikes, int noOfReads)
        {
            this.name = name;
            this.authorName = authorName;
            this.genre = genre;
            this.noOfChapters = noOfChapters;
            this.noOfLikes = noOfLikes;
            this.noOfReads = noOfReads;
        }
        public string Name
        {
            set { name = value; }
            get { return name; }
        }
        public string AuthorName
        {
            set { authorName = value; }
            get { return authorName; }
        }
        public string Genre
        {
            set { genre = value; }
            get { return genre; }
        }
        public int NoOfChapter
        {
            set { noOfChapters = value; }
            get { return noOfChapters; }
        }

        public int NoOfLikes
        {
            set { noOfLikes = value; }
            get { return noOfLikes; }
        }

        public int NoOfReads
        {
            set { noOfReads = value; }
            get { return noOfReads; }
        }

        public int CompareTo(object obj)
        {
            Story story = (Story)obj;
            return this.Name.CompareTo(story.Name);
        }

        public override string ToString()
        {
            return string.Format(this.name + " " + " " + this.authorName + " " + this.genre
                + " " + this.noOfChapters + " " + this.noOfLikes + " " + this.noOfReads);
        }

    }
}



//storyBo class

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Requirement5
{
    class StoryBo
    {

        public static Story createStory(String detail)
        {
            string[] s = detail.Split(",");

            Story story = new Story(s[0], s[1], s[2], Convert.ToInt32(s[3]), Convert.ToInt32(s[4]), Convert.ToInt32(s[5]));

            return story;

        }
    }
}

//NoofReadscomparater class


using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Requirement5
{
    class NoOfReadsComparator : IComparer<Story>
    {
        public int Compare(Story x, Story y)
        {
            return x.NoOfReads.CompareTo(y.NoOfReads);
        }
    }
}
