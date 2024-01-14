# memoize


	memoizer := memoize.NewMemoizer(0, 0)

const (
	propertyJourneyConfigCacheKey = "propertyJourneyConfig:%s"
)

func PropertyJourneyConfigCacheKey(propertyID string) string {
	return fmt.Sprintf(propertyJourneyConfigCacheKey, propertyID)
}


func (s Service) GetAllEnabledConfigsByPropertyID(ctx context.Context, propertyID string) ([]entity.JourneyConfig, error) {
	result, err, _ := s.memoizer.Memoize(PropertyJourneyConfigCacheKey(propertyID), func() (interface{}, error) {
		return s.journeyRepository.GetAllEnabledConfigsByPropertyID(ctx, propertyID)
	})

	return result.([]entity.JourneyConfig), err
}


s.memoizer.Delete(journeyservice.PropertyJourneyConfigCacheKey(journey.PropertyID))