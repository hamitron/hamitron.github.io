# Twiines
![splash](images/twiines_splash.png)
[Demo](http://boiling-tundra-5536.herokuapp.com/)
#### Twiines is a 'limited-scope microblogging platform' that focuses on sharing a chain of events such as a personal goal or project. These chains consist of goals and achievements and can be "twined" together with chains of other users.    
![timeline](images/twiines_timeline.png)

## Challenges:
* Route and understand complex model relationships in Rails and PostgreSQL.
* Configure Amazon Web Services to store user-uploaded photos.
* Sort and filter through multiple model objects for display.
* Structure timeline visual using CSS pseudo elements.

## Specs:
- PostgreSQL *formerly* MongoDB
- Rails 4

```ruby
# sorts milestones and stones in the timeline view based on value. Instead of separating them out, and having
# two loops showing milestones and stones this allows the view to render them all together and sort them accordingly.

	def combined_stone_mstone
		milestone_objects = self.milestones.all
		stone_objects = self.stones.all

		@combined_timeline_objects = milestone_objects + stone_objects

		@combined_timeline_objects = @combined_timeline_objects.sort {|m,s| s.sort_value <=> m.sort_value}
	end

```